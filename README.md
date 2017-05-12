# hello-world!This is first play github.now,the code is ajax and jsonp.
<!-- 以下方法为jquery实现 ajax请求 使用jsonp方法实现跨域 -->  
<script src="http://code.jquery.com/jquery-1.10.2.min.js"></script>  
  <script type="text/javascript">  
  jQuery(document).ready(function() {  
   $('#search_input').on('keyup',function(){  
        var searchText=$(this).val();  
        var getdata=function (data){  
        var d = data.AS.Results[0].Suggests;  
        var html = "";  
        // 将从服务器拿到的数据拼接成完整的html标签  
        for (var i = 0; i < d.length; i++) {  
             html += '<li>' + d[i].Txt + '</li>';  
         }  
        $('#suggest_result').html(html);  
        $('#suggest').css({  
            top:$('#search_form').offset().top+$('#search_form').height()+10,  
                left:$('#search_form').offset().left  
                //position:'absolute'  
                }).show();  
            };  
    $.ajax({  
        type:"GET",  
        url:"http://api.bing.com/qsonhs.aspx?type=cb&cb=getdata&q=" +searchText,  
        dataType: "jsonp",  
        async:false,  
        jsonp: "getdata",  
        jsonpCallback: "getdata",  
        success: function (data) {  
              getdata(data);  
           }  
        });  
    });  
    // 用户点击其他位置搜索框消失 提高用户体验  
  $(document).on('click',function(){  
    $('#suggest').hide();  
  });  
  // 事件代理 同时给多个元素绑定事件 并且这些节点是通过js动态生成的一般会用事件代理  
  //jquery的delegate()方法  
  // delegate() 方法为指定的元素（属于被选元素的子元素）添加一个或多个事件处理程序，并规定当这些事件发生时运行的函数  
  //使用 delegate() 方法的事件处理程序适用于当前或未来的元素（比如由脚本创建的新元素）。  
    $('#suggest').delegate('li','click', function () {    
            var keyword=$(this).text();    
           location.href='http://cn.bing.com/search?q='+keyword;    
        });    
    });   
