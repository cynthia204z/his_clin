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

  

- 承上(小駝峰)

  ```sql
  SELECT
      a.COLUMN_NAME,
      substr(replace(initcap('a'||lower(a.COLUMN_NAME)),'_',''),2),
      (a.DATA_TYPE || '(' || a.DATA_LENGTH || ')' ) AS DATA_TYPE,
      ( SELECT b.COMMENTS FROM user_col_comments b WHERE b.Table_Name = a.Table_Name AND b.column_name = a.column_name ) AS COMMENTS
  FROM user_tab_columns a
  WHERE a.Table_Name = 'MRM_EXAM_CHKLOG';
  ```




* inner join ... on ...

  ```sql
  select t.*,t1.SHEET_TYPE
  from CHRED_TRANS_MST t
  inner join chred_sheet_def t1 on t1.SHEET_ID = t.ShEET_ID
  where t1.SHEET_TYPE like '%text%';
  ```




HMS 片語建資料(Oracle)

```sql
update HMS_ITEM_PHRASE p set PHRASE_CONTENT =
    (
      select listagg(REPORT_CHNAME,',') within group ( order by REPORT_CHNAME) from HMS_REPORT_ITEMDTL t
      where t.ITEM_CODE=p.ITEM_CODE
      group by ITEM_CODE
    )

where p.ITEM_CODE in (
  'RIC200909051',
  'RIC200909070',
  'RIC200909162',
  'RIC200909166',
  'RIC201112002',
  'RIC201204001',
  'RIC201204002',
  'RIC201206001',
  'RIC201206002',
  'RIC201206003'
);
;
```

