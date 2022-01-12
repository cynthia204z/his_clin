```js
import axios from 'axios'
import { message } from '@/utils/message'
import store from '@/store'
import { getToken } from '@/utils/auth'
import define from '@/utils/define'


// create an axios instance
const service = axios.create({
  baseURL: process.env.VUE_APP_BASE_API, // url = base url + request url
  withCredentials: false, // send cookies when cross-domain requests
  timeout: define.timeout, // request timeout
})

// request interceptor
service.interceptors.request.use(
  config => {
    if (config.url.indexOf('http') > -1) config.baseURL = ''
    // 部分接口timeout時間單獨處理
    if (config.url.indexOf('SynThirdInfo') > -1 || config.url.indexOf('extend/Email/Receive') > -1 ||
      config.url.indexOf('Permission/Authority/Data') > -1 || config.url.indexOf('DataSync/Actions/Execute') > -1) {
      config.timeout = 100000
    }
    // do something before request is sent
    if (store.getters.token) {
      config.headers['Authorization'] = getToken()
    }
    if (config.method == 'get') {
      config.params = config.data
    }
    let timestamp = Date.parse(new Date()) / 1000
    if (config.url.indexOf('?') > -1) {
      config.url += `&n=${timestamp}`
    } else {
      config.url += `?n=${timestamp}`
    }
    return config
  },
  error => {
    // do something with request error
    if (process.env.NODE_ENV === 'development') {
      console.log(error) // for debug
    }
    return Promise.reject(error)
  }
)

// response interceptor
service.interceptors.response.use(
  response => {
    const res = response.data
    let config = response.config
    let url = config.url
    // 特殊接口處理
    if (url.indexOf('/Base/DataSource/Actions/Test') > -1 || (url.indexOf('Model') > -1 && url.indexOf('Config') > -1)) return res
    if (res.code !== 200) {
      message({
        message: res.msg || '請求出錯，請重試',
        type: 'error',
        duration: 1500,
        onClose: () => {
          if (url.indexOf('/api/oauth/Login') < 0 && url.indexOf('/api/oauth/LockScreen') < 0 && (res.code === 600 || res.code === 601 || res.code === 602)) {
            // 600：登錄過期,請重新登錄  601: 您的帳號在其他地方已登錄,被強制踢出 602: Token驗證失敗
            store.dispatch('user/resetToken').then(() => {
              if (window.location.pathname.indexOf('login') > -1) return
              setTimeout(() => { location.reload() }, 100);
            })
          }
        }
      })
      return Promise.reject(new Error(res.msg || 'Error'))
    } else {
      return res
    }
  },
  error => {
    if (process.env.NODE_ENV === 'development') {
      console.log(error) // for debug
    }
    message({
      message: '請求出錯，請重試',
      type: 'error',
      duration: 1500
    })
    return Promise.reject(error)
  }
)

export default service
```

