# SQL Note

- 該欄位有所種類的值

  ```sql
  select distinct OWNER_CODE from EMR_NOTE_PHRASE;
  ```

  

- 計算欄位中重複的值

  (`having (count(*) > 1)`是只列出有重複的)

  ```sql
  select OWNER_CODE, count(*) as count
  from EMR_NOTE_PHRASE where PHRASE_TYPE = 'Problem'
  group by OWNER_CODE
  -- having (count(*) > 1)
  ```

  

- HIS3用-欄位名/類型/註解

  ```sql
  select
      a.COLUMN_NAME,
      concat(a.DATA_TYPE,concat(concat('(',a.DATA_LENGTH),')')) as DATA_TYPE,
      b.COMMENTS
  from user_col_comments b
           left join user_tab_columns a
                     on  a.Table_Name=b.Table_Name
                         and  a.column_name=b.column_name
  where a.Table_Name='IER_PAT_PROBLEM';
  ```

  