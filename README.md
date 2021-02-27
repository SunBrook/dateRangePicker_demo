# dateRangePicker_demo
日期范围选择案例



> daterangepicker:	https://www.daterangepicker.cn/
>
> daterangepicker 指导：http://bsify.admui.com/daterangepicker/
>
> moment:	http://momentjs.cn/



## 示例代码

```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
    <meta charset="UTF-8">
    <title>时间段筛选demo</title>
    <link rel="stylesheet" href="css/daterangepicker.css">
    <link rel="stylesheet" href="css/daterangepicker.input.css">
    <script src="js/jquery-1.7.2.min.js"></script>
    <script src="js/moment.min.js"></script>
    <script src="js/zh-cn.js"></script>
    <script src="js/daterangepicker.js"></script>
</head>
<body>
<label for="daterange_publish">发布时间：</label>
<input type="text" id="daterange_publish" class="dateRangeInput" readonly="readonly"/>
</body>
</html>


<script type="text/javascript">
    var now = moment();
    var todayStart = moment([now.year(), now.month(), now.date()]);
    var todayEnd = now.endOf('day');

    //任务发布时间，默认今天0点到23点
    var pubOpDate = todayStart;
    var pubEdDate = todayEnd;
    
    //任务发布时间段
    $('#daterange_publish').daterangepicker({
        startDate: todayStart,
        endDate: todayEnd,
        maxDate: todayEnd, //最大值不能超过今天
        dateLimit: {
            months: 3 //最大时间间隔
        },
        opens: 'center',
        alwaysShowCalendars: true,
        timePicker: true,
        timePicker24Hour: true,
        //本地化
        locale: {
            format: 'YYYY/MM/DD HH:mm A',
            applyLabel: "确认",
            cancelLabel: "清空",
        }
    }).on('cancel.daterangepicker', function (ev, picker) {
        //取消
        $('#daterange_publish').val("");
        var hasValue = pubOpDate !== null || pubEdDate !== null;
        pubOpDate = null;
        pubEdDate = null;
        if (hasValue) {
            //刷新列表
            //loadPage();
        }
    }).on('apply.daterangepicker', function (ev, picker) {
        //确定
        pubOpDate = picker.startDate;
        pubEdDate = picker.endDate.seconds(59);

        //请求页面刷新
        //loadPage();
    });
</script>
```

