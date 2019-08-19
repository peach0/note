```fsh all dianxiao
fsh all dianxiao ssh "tail -f  /home/homework/clog/php/php-error.log"
fsh all dianxiao ssh "tail -f  /home/homework/log/laxin-sql/laxin_sql.log.slow.20190709* |grep laxindata |grep tblScFunnelTrans"
fsh all dianxiao ssh "cat /home/homework/log/laxin-sql/laxin_sql.log |grep tblScFunnelTrans"
fsh all dianxiao ssh "tail -f /home/homework/log/laxinquality/laxinquality.log | grep 200051"

fsh all cron-yike ssh "cat /tmp/dianxiao_PortraitImport.log*" 
查询cron一课的日志
```

