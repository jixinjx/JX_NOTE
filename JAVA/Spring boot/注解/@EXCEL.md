在Excel导出的时候，在实体类里面可以加的注解（@Excel自定义注解）

@JsonFormat(pattern="yyyy-MM-dd")设置年月日

@JsonFormat(pattern="yyyy-MM-dd HH:mm:ss")设置年月日时分秒（datetime）

@Excel(name="备注",dateFormat="yyyy-MM-dd")

@Excel(name="备注",dateFormat="yyyy-MM-dd HH:mm:ss")

@Excel(name="备注",readConverterExp="0=是,1=否")

这里的readConverterExp:如果数据库里面显示的是0/1那么在导出为Excel的时候显示的就是“是和否”。

加上Excel注解，数据库的字段才会在Excel的里面展示出来
