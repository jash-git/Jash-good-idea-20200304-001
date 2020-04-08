define("appmsg/wxtopic.js",["biz_wap/utils/ajax.js","biz_wap/jsapi/core.js","biz_common/dom/event.js","appmsg/topic_tpl.html.js"],function(t){
"use strict";
function e(t){
t.parentNode.removeChild(t);
}
function i(t,e){
var i=c;
e.img_url||(e.img_url=topic_default_img);
for(var o in e){
var a=new RegExp("{"+o+"}","g");
i=i.replace(a,e[o]);
}
var p=document.createElement("span");
p.className="db topic_area",p.innerHTML=i,t.parentNode.insertBefore(p,t),t.parentNode.removeChild(t),
r.tap(p,function(){
var e=location.protocol+"//mp.weixin.qq.com/mp/topic?action=topic_detail_page&topic_id="+t.getAttribute("data-topic-id")+"&topic_type="+t.getAttribute("data-topic-type")+"&sn="+t.getAttribute("data-topic-sn")+"&scene=101#wechat_redirect";
n.invoke("openUrlWithExtraWebview",{
url:e,
openType:1
},function(t){
t&&-1!==t.err_msg.indexOf(":ok")||(location.href=e);
});
});
}
function o(t){
var o={
topic_id:t.getAttribute("data-topic-id"),
topic_type:t.getAttribute("data-topic-type"),
sn:t.getAttribute("data-topic-sn"),
biz:biz
};
p({
url:"/mp/topic?action=get_topic_info",
type:"post",
data:o,
success:function(o){
if(console.log(o),o=JSON.parse(o),0!=o.base_resp.ret)return void e(t);
var a={
title:o.title,
author:o.author||(o.leading_actor?o.leading_actor.replace(/\$\$/g," / "):"-"),
img_url:o.img_url,
msg_num:o.msg_num
};
i(t,a);
},
error:function(){
e(t);
}
});
}
function a(){
var t=document.getElementsByTagName("wxtopic");
t[0]&&o(t[0]);
}
var p=t("biz_wap/utils/ajax.js"),n=t("biz_wap/jsapi/core.js"),r=t("biz_common/dom/event.js"),c=t("appmsg/topic_tpl.html.js");
a();
});define("question_answer/appmsg.js",["biz_common/utils/string/html.js","question_answer/appmsg_tpl.html.js","biz_wap/utils/ajax.js","question_answer/utils.js","biz_common/dom/event.js","appmsg/weapp_common.js","biz_common/tmpl.js","pages/utils.js","biz_wap/utils/mmversion.js"],function(t){
"use strict";
t("biz_common/utils/string/html.js");
var e=t("question_answer/appmsg_tpl.html.js"),a=t("biz_wap/utils/ajax.js"),n=t("question_answer/utils.js"),i=t("biz_common/dom/event.js"),o=t("appmsg/weapp_common.js"),r=t("biz_common/tmpl.js"),p=(t("pages/utils.js"),
t("biz_wap/utils/mmversion.js"),!1),s=navigator.userAgent.match(/MicroMessenger\/(\d+)\.(\d+)\.(\d+)/);
if(s){
var d=Number(s[1]),m=Number(s[2]),u=Number(s[3]);
d>6?p=!0:6===d&&m>5?p=!0:6===d&&5===m&&u>=3&&(p=!0);
}
var c={
weapp_username:"gh_f960dd3580ec@app",
detailPath:"pages/detail/index",
profilePath:"pages/list/index",
topicPath:"pages/themes/index",
canJumpOnTap:p,
questionType:[1,2,3,3,2,1],
data:{},
batchGetQuestionParam:null,
retry:1
},l=function(t){
return document.getElementById(t);
},g=function(){
var t=l("js_content");
if(!t)return!1;
for(var e=t.getElementsByTagName("mp-question")||[],a=0,n=e.length;n>a;a++){
var i=e[a],o=window.biz,r=i.getAttribute("data-mid"),p=i.getAttribute("data-idx"),s=i.getAttribute("data-type")||c.questionType[a],d=o+"_"+a;
c.data[d]?c.data[d].invisibleElems.push(i):c.data[d]=1===s?{
invisibleElems:[i],
type:s,
mid:r,
idx:p,
dataStatus:1
}:{
invisibleElems:[i],
type:s,
dataStatus:1
};
}
return 0===e.length?!1:!0;
},_=function(){
if(c.batchGetQuestionParam)return c.batchGetQuestionParam;
var t={
num:0
};
for(var e in c.data)if(Object.prototype.hasOwnProperty.call(c.data,e)){
var a=e.split("_");
t["__biz"+t.num]=a[0],1===c.data[e].type&&(t["mid"+t.num]=c.data[e].mid,t["idx"+t.num]=c.data[e].idx),
t["type"+t.num]=c.data[e].type,2===c.data[e].type&&(t["topic_id"+t.num]=1),t.num++;
}
return c.batchGetQuestionParam=t,c.batchGetQuestionParam;
},b=function(t){
var e="."+n.classPrefix;
i.on(t.dom,"tap",e+"show_detail_js",function(t){
{
var e=t.delegatedTarget,a=e.getAttribute("data-key"),n=(e.getAttribute("data-miniprogram-appid")||"wx3f84c32dc4b1e06b",
e.getAttribute("data-miniprogram-path")||c.detailPath+"?url="+encodeURIComponent(c.data[a].question_page_url)+"&bizNickname="+encodeURIComponent(c.data[a].biz_nickname));
e.getAttribute("data-miniprogram-title")||"";
}
c.canJumpOnTap?o.jumpUrl({
options:{
userName:c.weapp_username,
scene:1058,
sceneNote:encodeURIComponent(location.href),
relativeURL:o.getRelativeURL(n),
openType:2
},
beforeNonWechatWarn:function(){},
beforeJumpBackupPage:function(){},
onJsapiCallback:function(t){
"openWeApp:ok"===t.err_msg&&window.__addIdKeyReport&&window.__addIdKeyReport("28307",102);
}
}):console.log("cant jumpOnTap");
}),i.on(t.dom,"tap",e+"show_profile_js",function(t){
{
var e=t.delegatedTarget,a=(e.getAttribute("data-key"),e.getAttribute("data-miniprogram-appid")||"wx3f84c32dc4b1e06b",
e.getAttribute("data-miniprogram-path")||c.profilePath+"?biz="+encodeURIComponent(window.biz));
e.getAttribute("data-miniprogram-title")||"";
}
c.canJumpOnTap?o.jumpUrl({
options:{
userName:c.weapp_username,
scene:1058,
sceneNote:encodeURIComponent(location.href),
relativeURL:o.getRelativeURL(a),
openType:2
},
beforeNonWechatWarn:function(){},
beforeJumpBackupPage:function(){},
onJsapiCallback:function(t){
"openWeApp:ok"===t.err_msg&&window.__addIdKeyReport&&window.__addIdKeyReport("28307",102);
}
}):console.log("cant jumpOnTap");
}),i.on(t.dom,"tap",e+"show_theme_js",function(t){
{
var e=t.delegatedTarget,a=e.getAttribute("data-key"),n=(e.getAttribute("data-miniprogram-appid")||"",
e.getAttribute("data-miniprogram-path")||c.topicPath+"?themeId="+encodeURIComponent(c.data[a].themeId)+"&biz="+encodeURIComponent(window.biz));
e.getAttribute("data-miniprogram-title")||"";
}
c.canJumpOnTap?o.jumpUrl({
options:{
userName:c.weapp_username,
scene:1058,
sceneNote:encodeURIComponent(location.href),
relativeURL:o.getRelativeURL(n),
openType:2
},
beforeNonWechatWarn:function(){},
beforeJumpBackupPage:function(){},
onJsapiCallback:function(t){
"openWeApp:ok"===t.err_msg&&window.__addIdKeyReport&&window.__addIdKeyReport("28307",102);
}
}):console.log("cant jumpOnTap");
});
},f=function(t){
c.data[t.key]&&c.data[t.key].invisibleElems&&1*c.data[t.key].dataStatus!==1&&!function(){
var a=t.data||{};
a.dataStatus=c.data[t.key].dataStatus;
var n=c.data[t.key].invisibleElems.map(function(t){
var n=document.createElement("div"),i=r.tmpl(e,a,!0);
return n.innerHTML=i.trim(),t.parentNode.insertBefore(n.firstChild,t.nextsibling);
});
c.data[t.key].invisibleElems=null,n.length>0&&1*c.data[t.key].dataStatus===2&&n.forEach(function(e){
b({
dom:e,
allQuestionImg:t.data.allQuestionImg,
allAnswerImg:t.data.allAnswerImg
});
});
}();
},y=function(){},h=function v(){
a({
url:"/mp/qa?action=batch_get_qa_card",
type:"POST",
dataType:"json",
data:_(),
async:!0,
success:function(t){
t&&t.base_resp&&1*t.base_resp.ret===0&&"[object Array]"===Object.prototype.toString.call(t.qa_card_list)?(t.qa_card_list.forEach(function(e,a){
var i=e.biz_encode+"_"+a;
if(c.data[i]&&c.data[i].invisibleElems){
var o=n.formatQuestionInfo(e,t.svr_time,c.data[i].type);
o.dataKey=i;
var r=c.data[i].type;
c.data[i].qa_id=o.qa_id,1===r&&(c.data[i].biz_nickname=o.biz_nickname,c.data[i].question_page_url=o.question_page_url),
2===r&&(c.data[i].themeId=o.topicId),c.data[i].dataStatus=2,f({
data:o,
key:i
});
}
}),y(4)):y(3);
},
error:function(){
c.retry?(c.retry--,v()):y(3);
}
});
},w=function(){
g()&&h();
};
w();
});define("appmsg/weapp.js",["biz_common/utils/string/html.js","pages/weapp_tpl.html.js","biz_wap/utils/ajax.js","biz_common/dom/event.js","biz_common/tmpl.js","biz_common/dom/class.js","biz_wap/utils/device.js","appmsg/weapp_common.js","common/utils.js","biz_wap/utils/mmversion.js","biz_common/base64.js","appmsg/popup_report.js","biz_wap/utils/jsmonitor_report.js"],function(e){
"use strict";
function t(e,t,n){
var o=new Image;
o.src=("http://mp.weixin.qq.com/mp/jsreport?1=1&key=106&content="+n+",biz:"+biz+",mid:"+mid+",uin:"+uin+"[key1]"+encodeURIComponent(t.toString())+"&r="+Math.random()).substr(0,1024);
}
function n(e,t,n,o,i,p,a){
h({
url:"/mp/appmsgreport?action=appmsg_weapp_report",
data:{
__biz:window.biz||"",
mid:window.mid||"",
idx:window.idx||"",
weapp_appid:e||"",
weapp_pos:t||0,
weapp_title:o||0,
weapp_nickname:n||0,
type:i||0,
scene:window.source||-1,
weapp_type:p,
is_confirm:a||0,
ascene:window.ascene||-1
},
type:"POST",
dataType:"json",
async:!0,
success:function(){}
});
}
function o(e){
var t=e.innerHTML,n=/<img.*src=[\'\"]/,o=/background-image:(\s*)url\(/,i=/background:[^;"']+url\(/;
return n.test(t)||o.test(t)||i.test(t)?!0:!1;
}
function i(e){
var t=e.innerHTML,n=e.style.fontSize;
return 0===t.trim().length||0===parseFloat(n)?!0:!1;
}
function p(){
var e=u("js_content");
if(!e)return!1;
R=e.getElementsByTagName("mp-weapp")||[],x=e.getElementsByTagName("mp-miniprogram")||[],
K=[];
for(var t=e.getElementsByTagName("a"),n=0,o=t.length;o>n;n++){
var i=t[n],p=i.getAttribute("data-miniprogram-appid");
p&&K.push(i);
}
return R.length<=0&&x.length<=0&&0==K.length?!1:N&&0!=N.length?!0:(window.__addIdKeyReport&&window.__addIdKeyReport("27613","52",1),
!1);
}
function a(e){
return e=e||"",e.replace(/&/g,"&amp;").replace(/</g,"&lt;").replace(/>/g,"&gt;").replace(/"/g,"&quot;");
}
function r(e,t,o,i,p){
n(e,t,o,i,4,p),window.__addIdKeyReport&&window.__addIdKeyReport("28307",103);
}
function d(e,t,o,i,p){
n(e,t,o,i,5,p);
}
function s(){
function e(e){
e.preventDefault();
}
function p(e){
e&&(m=setTimeout(function(){
e.style.display="none",u=-1;
},100));
}
window.reportWeappid=[];
for(var s=0;s<N.length;s++)window.reportWeappid.push(N[s].appid);
var l=function(){};
y.on(document.getElementById("js_minipro_dialog_ok"),"click",function(t){
t.stopPropagation(),t.preventDefault(),document.querySelector("body").removeEventListener("touchmove",e);
var n=document.getElementById("js_minipro_dialog");
l&&l(),document.getElementById("js_minipro_dialog").style.display="none",B.report([4,1,"",img_popup?1:0,window.source,n._appid]);
}),y.on(document.getElementById("js_minipro_dialog_cancel"),"click",function(t){
t.stopPropagation(),t.preventDefault(),document.querySelector("body").removeEventListener("touchmove",e);
var o=document.getElementById("js_minipro_dialog");
o.style.display="none",n(o._appid,o._i,o._nickname,o._title,3,1,1),window.__addIdKeyReport&&window.__addIdKeyReport("28307",116),
B.report([3,1,"",img_popup?1:0,window.source,o._appid]);
}),y.on(document.getElementById("js_weapp_without_auth_dialog_ok"),"click",function(){
document.querySelector("body").removeEventListener("touchmove",e),document.getElementById("js_weapp_without_auth_dialog").style.display="none";
});
var m,u,h=j.os.pc,C=document.getElementById("js_pc_weapp_code"),z=document.getElementById("js_weapp_without_auth_dialog_mask"),R=document.getElementById("js_pc_weapp_code_img"),x=document.getElementById("js_pc_weapp_code_des");
h&&(y.on(C,"mouseenter",function(){
clearTimeout(m);
}),y.on(C,"mouseleave",function(){
p(C);
})),I.getAppidInfo({
onSuccess:function(j){
console.log("WeappCommon.getAppidInfo onsuccess");
var K=j.data.infoMap;
if(!K)return void(window.__addIdKeyReport&&window.__addIdKeyReport("27613","52",1));
for(s=0;s<A.length;s++)(function(s){
window.__addIdKeyReport("111535",1);
var k=A[s].appid,T=A[s].path,N=A[s].imageUrl,S=A[s].title,L=A[s].elem,M=K[k];
if(!M)return void(window.__addIdKeyReport&&window.__addIdKeyReport("27613","52",1));
var W=L.tagName.toLowerCase(),P=L.firstChild&&1==L.firstChild.nodeType&&"IMG"===L.firstChild.tagName;
if(P=P||L.firstElementChild&&"IMG"===L.firstElementChild.tagName,"a"!=W)L.innerHTML=v.tmpl(w,{
imageUrl:a(N),
title:a(S),
nickname:a(M.nickname),
avatar:a(M.logo_url)
});else{
if(P){
var U=L.firstChild;
U&&b.addClass(L,"weapp_image_link");
}else b.addClass(L,"weapp_text_link");
L.setAttribute("href","");
}
if(j.resp&&j.resp.weapp_info&&j.resp.weapp_info.length)for(var H=0;H<j.resp.weapp_info.length;H++){
var D=L.getElementsByClassName("guarantee_icon")[0];
if(j.resp.weapp_info[H].weapp_appid===k&&1===j.resp.weapp_info[H].has_guarantee_flag){
D&&b.addClass(D,"show");
break;
}
}
y.on(L,"tap",function(){
if(l=function(){
var e=P?1:"a"==W?2:0;
return I.jumpUrl({
sceneNote:encodeURIComponent(location.href),
appid:k,
path:T,
scene:window.__weapp_scene__||1058,
beforeNonWechatWarn:function(){
d(k,s,M.nickname,S,e);
},
beforeJumpBackupPage:function(){
r(k,s,M.nickname,S,e);
},
onJsapiCallback:function(e){
"openWeApp:ok"===e.err_msg&&window.__addIdKeyReport&&window.__addIdKeyReport("28307",102),
t(107,new Error(e.err_msg),"");
}
}),window.__addIdKeyReport&&window.__addIdKeyReport("28307",100),n(k,s,M.nickname,S,3,e,P?2:0),
P&&window.__addIdKeyReport&&window.__addIdKeyReport("28307",115),!1;
},E.isInMiniProgram&&-1===q.indexOf(k)&&E.gtVersion("7.0.5",!0)){
var p=document.getElementById("js_weapp_without_auth_dialog");
return p.style.display="block",document.querySelector("body").addEventListener("touchmove",e,{
passive:!1
}),document.getElementById("js_weapp_without_auth_weappurl").src="",I.getAppidCode({
appid:k,
path:T
},function(e){
document.getElementById("js_weapp_without_auth_weappurl").src=e;
}),!1;
}
if(P&&B.report([2,1,"",img_popup?1:0,window.source,k]),(P||b.hasClass(L,"weapp_text_link")&&(o(L)||i(L)))&&img_popup){
document.getElementById("js_minipro_dialog_head").innerText="即将打开小程序",document.getElementById("js_minipro_dialog_body").innerText=M.nickname;
var p=document.getElementById("js_minipro_dialog");
return p.style.display="block",document.querySelector("body").addEventListener("touchmove",e,{
passive:!1
}),p._appid=k,p._i=s,p._nickname=M.nickname,p._title=S,n(k,s,M.nickname,S,3,1,0),
I.canJumpOnTap&&window.__addIdKeyReport&&window.__addIdKeyReport("28307",114),!1;
}
return l();
},"a"==W),y.on(L,"click",function(e){
e.preventDefault(),e.stopPropagation();
},"a"==W),h&&(y.on(L,"mouseenter",function(){
function e(e){
function t(){
if(!m&&u===s){
C.style.display="block",m=!0;
var e=C.offsetHeight,t=C.offsetWidth;
"a"!=W||P?n>t?(g(C,"right-center"),C.style.left=n-t-l+"px",C.style.top=o+"px"):(g(C),
C.style.top=o+d-e-l+"px",C.style.left=n+r-t-l+"px"):(C.style.left=i>n+r/2-t/2?i+"px":n+r/2+t/2>i+p?i+p-t+"px":n+r/2-t/2+"px",
a>e?(g(C,"down-center"),C.style.top=o-e-l+"px"):(g(C,"up-center"),C.style.top=o+d-l+"px"));
}
}
if(e){
var n=c(L),o=_(P?L.firstElementChild:L),i=c(L.parentNode),p=L.parentNode.offsetWidth,a=L.getBoundingClientRect().top,r=P?L.firstElementChild.offsetWidth:L.offsetWidth,d=P?L.firstElementChild.offsetHeight:L.offsetHeight,l=8,m=!1;
x.innerText=f(M.nickname,48),R.onload=t,R.src=e,(R.complete||R.width)&&t();
}
}
clearTimeout(m),u!==s&&(C.style.display="none",u=s,I.getAppidCode({
appid:k,
path:T
},e));
}),y.on(L,"mouseleave",function(){
p(C);
})),E.isInMiniProgram&&-1===q.indexOf(k)&&E.gtVersion("7.0.5",!0)&&y.on(z,"click",function(){
var t=document.getElementById("js_weapp_without_auth_dialog");
document.querySelector("body").removeEventListener("touchmove",e),t.style.display="none";
});
})(s);
var T=null,N=function(){
T=null;
for(var e=0;e<S.length;e++){
var t=S[e].elem,o=t.tagName.toLowerCase(),i=t.firstChild&&1==t.firstChild.nodeType,p=i?1:"a"==o?2:0,a=S[e].elem.getBoundingClientRect();
if(a.top<k.getInnerHeight()&&a.bottom>0){
setTimeout(function(){
window.__addIdKeyReport&&window.__addIdKeyReport("28307",101);
},0);
var r=S[e].appid;
r&&K[r]&&K[r].nickname&&n(r,e,K[r].nickname,S[e].title,2,p),S.splice(e--,1);
}
}
};
N(),y.on(window,"scroll",function(){
T||(T=setTimeout(N,100));
});
},
onError:function(e){
3==e.code&&t(106,e.catchErr,"parsing weapp info error");
}
});
}
function l(){
for(var e=0,t=0;t<x.length+R.length;t++){
var n=t<x.length,o=n?x[t]:R[t-x.length],i=o.getAttribute(n?"data-miniprogram-appid":"data-weapp-appid")||"",p=o.getAttribute(n?"data-miniprogram-path":"data-weapp-path")||"",a=o.getAttribute(n?"data-miniprogram-imageUrl":"data-weapp-imageUrl")||"",r=o.getAttribute(n?"data-miniprogram-title":"data-weapp-title")||"",d=document.createElement("span");
o.setAttribute("class",""),d.setAttribute("class","weapp_display_element js_weapp_display_element"),
A.push({
appid:i,
path:p,
imageUrl:a,
title:r,
elem:d
}),S.push({
appid:i,
elem:d,
title:r
}),o.parentNode.insertBefore(d,o.nextSibling),m(a)||e++;
}
for(var t=0;t<K.length;t++){
var s=K[t];
A.push({
appid:s.getAttribute("data-miniprogram-appid"),
path:s.getAttribute("data-miniprogram-path")||"",
elem:s
});
}
e>0&&z.setSum(64469,33,e);
}
function m(e){
for(var t,n=[/^http(s)?:\/\/mmbiz\.qpic\.cn([\/?].*)*$/i,/^http(s)?:\/\/mmbiz\.qlogo\.cn([\/?].*)*$/i,/^http(s)?:\/\/mmsns\.qpic\.cn([\/?].*)*$/i],o=0;t=n[o++];)if(t.test(e))return!0;
return!1;
}
function u(e){
return document.getElementById(e);
}
function c(e){
for(var t=0;e;)t+=e.offsetLeft,e=e.offsetParent;
return t;
}
function _(e){
for(var t=0;e;)t+=e.offsetTop,e=e.offsetParent;
return t;
}
function g(e,t){
for(var n=0;3>n;n++)b.removeClass(e,"weui-desktop-popover_pos-up-"+L[n]),b.removeClass(e,"weui-desktop-popover_pos-down-"+L[n]),
b.removeClass(e,"weui-desktop-popover_pos-left-"+M[n]),b.removeClass(e,"weui-desktop-popover_pos-right-"+M[n]);
b.removeClass(e,"weui-desktop-popover_hide-arrow"),t?b.addClass(e,"weui-desktop-popover_pos-"+t):b.addClass(e,"weui-desktop-popover_hide-arrow");
}
function f(e,t){
var n=/[^\x00-\xff]/g;
if(e.replace(n,"**").length>t)for(var o=Math.floor(t/2),i=o,p=e.length;p>i;i++)if(e.substring(0,i).replace(n,"**").length>=t)return e.substring(0,i)+"...";
return e;
}
e("biz_common/utils/string/html.js");
var w=e("pages/weapp_tpl.html.js"),h=e("biz_wap/utils/ajax.js"),y=e("biz_common/dom/event.js"),v=e("biz_common/tmpl.js"),b=e("biz_common/dom/class.js"),j=e("biz_wap/utils/device.js"),I=e("appmsg/weapp_common.js"),k=e("common/utils.js"),E=e("biz_wap/utils/mmversion.js"),C=e("biz_common/base64.js"),B=e("appmsg/popup_report.js"),z=e("biz_wap/utils/jsmonitor_report.js"),R=null,x=null,K=null,T={},A=[],N=I.appidSnInfo,S=[],q=C.fromBase64(appid_list).split(",");
if(p()){
l(),s();
var L=["left","center","right"],M=["top","center","bottom"];
return T;
}
});define("appmsg/weproduct.js",["appmsg/weapp_common.js","biz_common/dom/event.js","biz_wap/utils/ajax.js","biz_common/utils/url/parse.js","biz_wap/utils/jsmonitor_report.js","common/utils.js"],function(t){
"use strict";
function e(){
if(console.log("weproduct init"),"function"==typeof document.getElementsByClassName){
var t=document.getElementsByClassName("js_product_container");
t&&t.length>0&&(a(t),d.getAppidInfo({
onSuccess:function(e){
g.data=e.data,o(t);
}
})),r();
}
}
function a(t){
try{
for(var e=0,a=t.length;a>e;e++){
var o=t[e];
if(o.className.indexOf("js_list_container")>=0){
var i=o.querySelector("img.js_cover");
if(i){
var r=i.parentNode.getBoundingClientRect();
i.style.setProperty("width",r.width+"px","important"),i.style.setProperty("height",r.height+"px","important"),
i.style.setProperty("background-size","unset","important"),"0"==i.getAttribute("data-fail")?n.call(i):i.getAttribute("data-fail")||(i.lazyLoadOnload=i.lazyLoadOnload||[],
i.lazyLoadOnload.push(n));
}
}
}
}catch(p){}
}
function n(){
var t=this.parentNode;
if(t){
var e=document.createElement("span");
e.className=this.className,e.style.background='url("'+this.src+'") no-repeat center',
t.insertBefore(e,this),t.removeChild(this);
}
}
function o(t){
for(var e=0,a=t.length;a>e;e++)!function(t,e){
s.on(t,"tap",".js_product_loop_content",function(t){
var a=t.delegatedTarget,n=a.getAttribute("data-wxaappid"),o=a.getAttribute("data-wxapath"),i=a.getAttribute("data-pid"),r=a.getAttribute("data-appid");
return d.jumpUrl({
privateExtraData:{
cookies:"cps_package=123456; expires=1538286412; busid=mmbiz_ad_cps; domain=*"
},
sourceAppId:r,
appid:n,
path:o,
scene:1091,
sceneNote:encodeURIComponent(location.href)+":"+encodeURIComponent(i),
beforeNonWechatWarn:function(){},
beforeJumpBackupPage:function(){},
onJsapiCallback:function(t){
if("openWeApp:ok"===t.err_msg&&i){
var o=a.getAttribute("data-pidtype"),r=2;
2==o&&(r=4),p([{
wxa_appid:n,
pid:i,
type:r,
absolute_order:e+1,
appid:a.getAttribute("data-appid")||"",
templateid:a.getAttribute("data-templateid")||"",
relative_order:1*a.getAttribute("data-order"),
packid:a.getAttribute("data-packid")||""
}]);
}
}
}),!1;
});
}(t[e],e);
var n=document.getElementsByClassName("js_product_loop_content");
if(n&&n.length>0&&m.getInnerHeight()){
for(var e=0;e<n.length;e++)g.pvele.push(n[e]);
i(),s.on(window,"scroll",i);
}
}
function i(){
g.checkInScreenId&&clearTimeout(g.checkInScreenId),g.checkInScreenId=setTimeout(function(){
g.checkInScreenId=null;
for(var t=[],e=0;e<g.pvele.length;e++){
var a=g.pvele[e],n=a.getBoundingClientRect(),o=n.height||n.bottom-n.top;
if(o>0&&n.top<m.getInnerHeight()&&n.bottom>0){
var r=a.getAttribute("data-pid");
if(r){
var d=a.getAttribute("data-pidtype"),c=1;
2==d&&(c=3),t.push({
wxa_appid:a.getAttribute("data-wxaappid"),
pid:r,
type:c,
absolute_order:e+1,
appid:a.getAttribute("data-appid")||"",
templateid:a.getAttribute("data-templateid")||"",
relative_order:1*a.getAttribute("data-order"),
packid:a.getAttribute("data-packid")||""
});
}
g.pvele.splice(e--,1);
}
}
p(t),0==g.pvele.length&&(s.off(window,"scroll",i),i=null);
},100);
}
function r(){
setTimeout(function(){
var t=document.getElementsByClassName("js_product_loop_content").length,e=document.getElementsByClassName("js_product_err_container").length;
u.setSum("64469","15",t+e),u.setSum("64469","16",t),u.setSum("64469","18",e);
},0);
}
function p(t){
if(t&&0!=t.length){
for(var e={
batch_no:l.getQuery("batch_no")||"",
bizuin:window.biz||"",
biz:window.biz||"",
mid:window.mid||"",
idx:window.idx||"",
total:t.length
},a=0;a<t.length;a++){
var n=t[a],o=a+1;
for(var i in n)n.hasOwnProperty(i)&&(e[i+""+o]=n[i]);
}
c({
url:"/mp/productreport?",
type:"POST",
data:e,
dataType:"json",
async:!0
});
}
}
var d=t("appmsg/weapp_common.js"),s=t("biz_common/dom/event.js"),c=t("biz_wap/utils/ajax.js"),l=t("biz_common/utils/url/parse.js"),u=t("biz_wap/utils/jsmonitor_report.js"),m=t("common/utils.js"),g={
pvele:[],
checkInScreenId:null,
reportRandom:Math.random()
};
e();
});define("appmsg/voicemsg.js",["biz_wap/jsapi/core.js","biz_common/dom/event.js","biz_common/dom/class.js"],function(e){
"use strict";
function o(e){
return document.getElementById(e);
}
function i(){
"1"==window.show_msg_voice&&(s.invoke("getBackgroundAudioState",{},function(e){
console.log("voicemsg getBackgroundAudioState res",e);
var i="waiting"==e.playState||"seeked"==e.playState||"seeking"==e.playState||"play"==e.playState;
e.paused=1*e.paused,e&&!e.paused&&i&&e.src&&e.src.indexOf("/mp/msgvoice?action=get_voice")>=0?a||(o("js_msgvoice_reading").style.display="",
o("js_msgvoice_reading_title").innerHTML=e.title,console.log("hello msgvoice reading"),
n.on(o("js_msgvoice_reading"),"click",function(){
location.href=e.musicbar_url||"https://mp.weixin.qq.com/mp/msgvoice?action=ttspage&__biz="+window.biz+"&mid="+window.mid+"&idx="+window.idx+"&sn="+window.sn+"#wechat_redirect";
}),c.addClass(o("page-content"),"voice"),console.log("add class voice in page-content"),
a=!0):(a=!1,o("js_msgvoice_reading").style.display="none",c.removeClass(o("page-content"),"voice"),
console.log("removeClass done"));
}),console.log("begin to getBackgroundAudioState in show_msg_voice"),setTimeout(function(){
i(),4>=d&&(d++,t+=1e3);
},t)),console.log("show_msg_voice is",window.show_msg_voice);
}
var s=e("biz_wap/jsapi/core.js"),n=e("biz_common/dom/event.js"),c=e("biz_common/dom/class.js"),t=1e3,a=!1,d=0;
i();
});define("appmsg/autoread.js",["biz_common/utils/string/html.js","biz_common/dom/event.js","pages/voice_tpl.html.js","pages/voice_component.js","biz_wap/utils/ajax.js"],function(e){
"use strict";
function i(){
var e=d("autoread");
e&&(e.innerHTML='<p><label>朗读类型：</label>                                <select id="autoreadSelect">                                <option selected="true" value="0">女1</option>                                <option value="1">女2</option>                                <option value="2">男1</option>                                <option value="6">男2</option>                                </select></p><p id="autoread_voice"></p>',
r.on(d("autoreadSelect"),"change",function(){
p.player&&(p.player.destory(),p.player=null),p.checkAudioId&&(clearTimeout(p.checkAudioId),
p.checkAudioId=null);
var e=d("autoreadSelect");
d("autoread_voice").innerHTML="",o(e.value);
}),o(0));
}
function o(e){
var i=d("autoread_voice");
p._oMusic={
voiceid:p.voiceid,
duration_str:"",
posIndex:p.posIndex,
title:"文章朗读体验（"+p.voiceType[e||0]+"）",
nickname:window.nickname||"公众号"
},s.renderPlayer(u,p._oMusic,i,!0),d("voice_author_"+p.key).innerHTML="来自"+p._oMusic.nickname+"（创建音频中）",
c(e);
}
function n(e,i){
var o=p._oMusic;
d("voice_author_"+p.key).innerHTML="来自"+o.nickname,d("voice_duration_"+p.key).innerHTML=s.formatTime(1*i),
p.player=s.init({
protocal:"hls",
wxIndex:o.posIndex,
type:2,
songId:e,
src:a("https://mp.weixin.qq.com/mp/msgvoice?action=get_voice&media="+e),
allowPause:!0,
autoPlay:!0,
duration:i,
title:o.title,
singer:o.nickname?o.nickname+"的语音":"公众号语音",
epname:"来自文章",
coverImgUrl:window.__appmsgCgiData.hd_head_img,
playingCss:"share_audio_playing",
playCssDom:d("voice_main_"+p.key),
playArea:d("voice_play_"+p.key),
progress:d("voice_progress_"+p.key),
fileSize:o.fileSize,
playtimeDom:d("voice_playtime_"+p.key),
bufferDom:d("voice_buffer_"+p.key),
playdotDom:d("voice_playdot_"+p.key),
seekRange:d("voice_seekRange_"+p.key),
seekContainer:d("voice_main_"+p.key),
loadingDom:d("voice_loading_"+p.key)
});
}
function t(e){
p.curNum+=1;
var i=1e3;
p.curNum>p.maxNum&&(i=2e3);
var o=["/mp/msgvoice?action=get_media&mid=",window.mid||"","&idx=",window.idx||"","&biz=",window.biz||"","&type=",e||0].join("");
m({
url:o,
type:"GET",
dataType:"json",
async:!0,
success:function(o){
o.mediaid&&o.duration?n(o.mediaid,o.duration):p.checkAudioId=setTimeout(function(){
t(e);
},i);
},
error:function(){
p.checkAudioId=setTimeout(function(){
t(e);
},i);
}
});
}
function a(e){
return e+=["&mid=",window.mid||"","&idx=",window.idx||"","&biz=",window.biz||"","&uin=",window.uin||"","&key=",window.key||"","&pass_ticket=",window.pass_ticket||"","&clientversion=",window.clientversion||"","&devicetype=",window.devicetype||"","&wxtoken=",window.wxtoken||""].join("");
}
function c(e){
p.curNum=0;
var i=["/mp/msgvoice?action=tts&mid=",window.mid||"","&idx=",window.idx||"","&biz=",window.biz||"","&type=",e||0].join("");
m({
url:i,
type:"GET",
dataType:"json",
async:!0,
success:function(i){
i&&i.base_resp&&0==i.base_resp.ret?t(e):d("voice_author_"+p.key).innerHTML="来自"+window.nickname+"（失败）";
},
error:function(){
d("voice_author_"+p.key).innerHTML="来自"+window.nickname+"（失败）";
}
});
}
function d(e){
return document.getElementById(e);
}
e("biz_common/utils/string/html.js");
var r=e("biz_common/dom/event.js"),u=e("pages/voice_tpl.html.js"),s=e("pages/voice_component.js"),m=e("biz_wap/utils/ajax.js"),p={
checkId:"",
voiceid:"autoread",
posIndex:0,
key:"autoread_0",
voiceType:{
0:"女1",
1:"女2",
2:"男1",
6:"男2"
},
maxNum:5,
curNum:0
};
i();
});define("redpackage/redpacketcover.js",["biz_common/utils/string/html.js","redpackage/tpl/card_tpl.html.js","biz_common/dom/event.js","biz_wap/jsapi/core.js","biz_common/tmpl.js","common/utils.js","common/comm_report.js","pages/player_tips.js","biz_common/utils/url/parse.js","biz_wap/utils/mmversion.js","biz_wap/utils/ajax.js"],function(e){
"use strict";
e("biz_common/utils/string/html.js");
var t=e("redpackage/tpl/card_tpl.html.js"),a=e("biz_common/dom/event.js"),r=e("biz_wap/jsapi/core.js"),i=e("biz_common/tmpl.js"),o=e("common/utils.js"),n=e("common/comm_report.js"),d=e("pages/player_tips.js"),s=e("biz_common/utils/url/parse.js"),c=e("biz_wap/utils/mmversion.js"),u=e("biz_wap/utils/ajax.js"),p={
tagName:"redpacketcover",
isWechat:c.isWechat,
domMap:{},
dataMap:{},
startTime:window.page_begintime||0,
screen_height:o.getInnerHeight(),
screen_num:0,
pvData:[],
request_id:encodeURIComponent(window.biz+";"+window.mid+";"+window.idx+";"+window.page_begintime||0),
hasBindVisibility:!1,
hasBindScroll:!1,
needReportNum:0,
reportedNum:0
},m=function(){
var e=arguments.length<=0||void 0===arguments[0]?{}:arguments[0],t=window.pageYOffset||document.documentElement.scrollTop,a=(window.logs.read_height||t)+p.screen_height,r={
BizUin:window.biz,
MsgId:1*window.mid,
Idx:1*window.idx,
CoverUri:e.coverUri,
Scene:1*window.source,
Subscene:1*window.subscene,
CoverStatus:1*e.coverStatus,
EventType:1*e.eventType,
EventScreenNum:Math.ceil(a/p.screen_height)||1,
ScreenNum:p.screen_num,
StartTimeMs:p.startTime
};
n.report(19119,r);
},l=function(){
for(var e=window.pageYOffset||document.documentElement.scrollTop,t=e+p.screen_height,r=0;r<p.pvData.length;r++){
var i=p.pvData[r];
t>=i.start&&t<=i.end&&(p.reportedNum++,p.dataMap&&p.dataMap[i.coverUri]&&(p.dataMap[i.coverUri].reported=!0),
m({
eventType:2,
coverUri:i.coverUri,
coverStatus:p.dataMap[i.coverUri].status
}),p.pvData.splice(r,1),r--);
}
p.reportedNum>=p.needReportNum&&(a.off(window,"scroll",l),p.pvData=[],l=null);
},v=function(){
p.pvData.length>0&&(!p.hasBindScroll&&l&&(p.hasBindScroll=!0,a.on(window,"scroll",l)),
l());
},_=function(){
var e=arguments.length<=0||void 0===arguments[0]?{}:arguments[0];
if(p.isWechat){
p.scroll_height=document.body.scrollHeight||document.body.offsetHeight,p.screen_num=Math.ceil(p.scroll_height/p.screen_height);
var t=e.node;
if(p.dataMap[e.coveruri]&&1*p.dataMap[e.coveruri].status!==-1&&!p.dataMap[e.coveruri].reported){
var a=t.getBoundingClientRect();
p.pvData.push({
start:a.top+a.height/2,
end:a.top+a.height/2+p.screen_height,
coverUri:e.coveruri
});
}
v();
}
},g=null,h=function(){
var e=arguments.length<=0||void 0===arguments[0]?{}:arguments[0];
p.dataMap[e.coveruri]&&a.on(e.dom,"click",function(){
window.is_temp_url?new d({
msg:"预览时不支持领取红包封面"
}):p.isWechat?!function(){
var t=e.dom.getAttribute("data-coveruri")||"",a=t&&p.dataMap[t]?p.dataMap[t].redirect_url:"";
a&&(m({
eventType:1,
coverUri:t,
coverStatus:p.dataMap[t].status
}),r.invoke("openUrlWithExtraWebview",{
url:a,
openType:1
},function(e){
-1===e.err_msg.indexOf("ok")&&(location.href=a);
}));
}():new d({
msg:"请在微信客户端打开"
});
}),!p.hasBindVisibility&&p.isWechat&&(p.hasBindVisibility=!0,o.listenStateChange({
cb:function(e){
("onResume"===e.state_change||"onResume"===e.state)&&u({
type:"GET",
dataType:"json",
url:"/mp/wapredpacketcover?action=get_red_packet_cover_data&__biz="+window.biz+"&mid="+window.mid+"&idx="+window.idx+"&sn="+window.sn+"&send_time="+window.send_time,
timeout:1e4,
success:function(e){
if(e&&e.base_resp&&1*e.base_resp.ret===0&&e.red_packet_cover_data&&e.red_packet_cover_data.cover_uri_data&&e.red_packet_cover_data.cover_uri_data.length>0)for(var t=e.red_packet_cover_data.cover_uri_data,a=0,r=t.length;r>a;a++){
var i=t[a],o=p.domMap[i.cover_uri],n=p.dataMap[i.cover_uri];
if(n&&o){
var d=1*n.status,s=1*i.status;
-1!==s&&d!==s&&(n.status=s,g({
data:n,
node:o,
isUpdate:!0
}));
}
}
}
});
}
}));
};
g=function(){
var e=arguments.length<=0||void 0===arguments[0]?{}:arguments[0];
e.node&&e.data&&e.data.cover_uri&&(e.isUpdate?e.node.innerHTML=i.tmpl(t,{
data:e.data,
isUpdate:!0
}).replace(/>\s*</g,"><").replace(/^\s+/,"").replace(/\s+$/,""):e.data.receive_image&&!function(){
var a=function(e){
var a=e.node,r=e.data;
return function(){
var e=document.createElement("div");
e.innerHTML=i.tmpl(t,{
data:r,
isUpdate:!1
}).replace(/>\s*</g,"><").replace(/^\s+/,"").replace(/\s+$/,"");
var o=e.firstChild;
a.parentNode.insertBefore(o,a.nextSibling);
var n=a.parentNode.querySelector('[data-preloadingid="'+r.cover_uri+'"]');
n&&n.parentNode.removeChild(n),p.domMap[r.cover_uri]=o,h({
dom:o,
coveruri:r.cover_uri
}),_({
coveruri:r.cover_uri,
node:o
});
};
}(e),r=function(){
this.onload=null,this.onerror=null,a();
},o=new Image;
o.onload=r,o.onerror=r,o.src=e.data.receive_image;
}());
};
var w=function(){
var e=arguments.length<=0||void 0===arguments[0]?{}:arguments[0];
if(e.list&&0!==e.list.length){
for(var t=0,a=e.list.length;a>t;t++){
var r=e.list[t];
p.dataMap[r.cover_uri]=r;
}
var i=document.querySelectorAll(p.tagName);
e.list.length!==i.length&&window.__addIdKeyReport&&window.__addIdKeyReport("27613","51",1),
p.needReportNum=i.length;
for(var t=0,a=i.length;a>t;t++){
var r=i[t],o=r.getAttribute("data-coveruri")||"",n=decodeURIComponent(o),d=p.dataMap[n];
if(d&&1*d.status!==-1){
if(d.redirect_url){
var c=d.redirect_url.html(!1);
c=s.addParam(c,"request_id",p.request_id,!0);
var u=s.parseUrl(c);
u.hash?-1===u.hash.indexOf("wechat_redirect")&&(c+="&wechat_redirect"):c+="#wechat_redirect",
d.redirect_url=c;
}
g({
data:d,
node:r,
isUpdate:!1
});
}
}
}
},f=function(){
var e=document.querySelectorAll(p.tagName);
if(!window.__appmsgCgiData||1*window.__appmsgCgiData.has_red_packet_cover!==1)return void(e.length>0&&window.__addIdKeyReport&&window.__addIdKeyReport("27613","51",1));
if(!p.isWechat)for(var t=0,a=e.length;a>t;t++){
var r=e[t],i=r.getAttribute("data-coveruri")||"",o=decodeURIComponent(i),n=decodeURIComponent(r.getAttribute("data-receiveimg")||"");
if(o&&n&&/^http(s)?:\/\/mmcomm\.qpic\.cn([\/?].*)*$/i.test(n)){
var d={
cover_uri:o,
status:0,
name:"",
redirect_url:"",
receive_image:n
};
p.dataMap[o]=d,g({
data:d,
node:r,
isUpdate:!1
});
}
}
};
return f(),{
render:w
};
});define("appmsg/voice.js",["biz_common/utils/string/html.js","pages/voice_tpl.html.js","appmsg/log.js","pages/voice_component.js"],function(e){
"use strict";
function i(){
var e=a("js_content");
return e?(p._oElements=e.getElementsByTagName("mpvoice")||[],p._oElements.length<=0?!1:!0):!1;
}
function o(){
p.musicLen=p._oElements.length;
}
function n(){
for(var e=0,i=0;i<p.musicLen;i++){
var o=p._oElements[i],n={},c=o.getAttribute("voice_encode_fileid")||"";
try{
c=decodeURIComponent(c);
}catch(a){}
n.voiceid=r.encodeStr(c),n.voiceid=n.voiceid.replace(/&#61;/g,"=").replace(/^\s/,"").replace(/\s$/,""),
n.isaac=1*o.getAttribute("isaac2")||0,n.src=p.srcRoot.replace("#meidaid#",n.voiceid),
1===n.isaac&&(n.jsapi2Src=n.src+"&voice_type=1"),n.voiceid&&"undefined"!=n.voiceid&&(t(o,n,e),
e++);
}
}
function t(e,i,o){
i.duration=parseInt((1*e.getAttribute("play_length")||0)/1e3,10),i.duration_str=r.formatTime(i.duration),
i.posIndex=o;
var n=e.getAttribute("name")||"";
try{
n=decodeURIComponent(n);
}catch(t){}
i.title=r.encodeStr(n).replace(/^\s/,"").replace(/\s$/,""),i.fileSize=1*e.getAttribute("high_size")||0,
i.nickname=window.nickname,r.renderPlayer(d,i,e);
var a=i.voiceid+"_"+i.posIndex,s=e.parentNode.querySelector('[data-preloadingid="'+a+'"]');
s&&s.parentNode.removeChild(s),c(i),p.musicList[i.voiceid+"_"+i.posIndex]=i;
}
function c(e){
var i=e.voiceid+"_"+e.posIndex,o="";
if(window.voice_in_appmsg&&window.voice_in_appmsg[e.voiceid]){
var n=window.voice_in_appmsg[e.voiceid],t=window.biz||"",c=window.mid||"",d=window.idx||"";
n.bizuin&&n.appmsgid&&n.idx&&(t=n.bizuin,c=n.appmsgid,d=n.idx);
var p=window.location.protocol||"https:";
o=p+"//mp.weixin.qq.com/mp/audio?_wxindex_=#_wxindex_#&scene=104&__biz=#biz#&mid=#mid#&idx=#idx#&voice_id=#voice_id#&sn=#sn##wechat_redirect".replace("#_wxindex_#",e.posIndex).replace("#biz#",t).replace("#mid#",c).replace("#idx#",d).replace("#voice_id#",e.voiceid).replace("#sn#",n.sn||"");
}
s("[Voice] init"+o);
var m=r.decodeStr(e.title);
e.player=r.init({
wxIndex:e.posIndex,
type:2,
songId:e.voiceid,
comment_id:"",
src:e.src,
jsapi2Src:e.jsapi2Src,
allowPause:!0,
duration:e.duration,
title:m,
singer:window.nickname?window.nickname+"的语音":"公众号语音",
epname:"来自文章",
coverImgUrl:window.__appmsgCgiData.hd_head_img,
playingCss:"share_audio_playing",
playCssDom:a("voice_main_"+i),
playArea:a("voice_play_"+i),
progress:a("voice_progress_"+i),
fileSize:e.fileSize,
playtimeDom:a("voice_playtime_"+i),
bufferDom:a("voice_buffer_"+i),
playdotDom:a("voice_playdot_"+i),
seekRange:a("voice_seekRange_"+i),
seekContainer:a("voice_main_"+i),
loadingDom:a("voice_loading_"+i),
detailArea:o?a("voice_main_"+i):"",
detailUrl:o,
webUrl:o
});
}
function a(e){
return document.getElementById(e);
}
e("biz_common/utils/string/html.js");
var d=e("pages/voice_tpl.html.js"),s=e("appmsg/log.js"),r=e("pages/voice_component.js"),p={
musicList:{},
musicLen:0,
srcRoot:location.protocol+"//res.wx.qq.com/voice/getvoice?mediaid=#meidaid#"
};
return i()?(o(),n(),p.musicList):void 0;
});define("appmsg/qqmusic.js",["biz_common/utils/string/html.js","biz_common/utils/url/parse.js","appmsg/log.js","pages/qqmusic_tpl.html.js","pages/voice_component.js","pages/qqmusic_ctrl.js","pages/kugoumusic_ctrl.js"],function(e){
"use strict";
function t(){
var e=u("js_content");
return e?(p._oElements=e.getElementsByTagName("qqmusic")||[],p._oElements.length<=0?!1:!0):!1;
}
function i(){
p.musicLen=p._oElements.length;
}
function s(){
for(var e=0,t=0;t<p.musicLen;t++){
var i=p._oElements[t],s={};
s.musicid=l.encodeStr(i.getAttribute("musicid")||"").replace(/^\s/,"").replace(/\s$/,""),
s.musicid&&"undefined"!=s.musicid&&(r(i,s,e),e++);
}
}
function r(e,t,i){
if(t.media_id=l.encodeStr(e.getAttribute("mid")||"").replace(/^\s/,"").replace(/\s$/,""),
t.musictype=parseInt(e.getAttribute("musictype"))||1,t.musictype>2&&(t.musictype=2),
t.albumid=l.encodeStr(e.getAttribute("albumid")||"").replace(/^\s/,"").replace(/\s$/,""),
t.otherid=l.encodeStr(e.getAttribute("otherid")||"").replace(/^\s/,"").replace(/\s$/,""),
t.jumpurlkey=l.encodeStr(e.getAttribute("jumpurlkey")||"").replace(/^\s/,"").replace(/\s$/,""),
t.duration=parseInt(e.getAttribute("play_length")||0,10),t.posIndex=i,t.albumurl=l.encodeStr(e.getAttribute("albumurl")||"").replace(/^\s/,"").replace(/\s$/,""),
t.audiourl=l.encodeStr(e.getAttribute("audiourl")||"").replace(/^\s/,"").replace(/\s$/,""),
t.singer=l.encodeStr(e.getAttribute("singer")||"").replace(/^\s/,"").replace(/\s$/,""),
!t.singer||"undefined"==t.singer){
var s=e.getAttribute("src")||"",r=decodeURIComponent(a.getQuery("singer",s)||"");
t.singer=l.encodeStr(r).replace(/^\s/,"").replace(/\s$/,""),t.singer&&"undefined"!=t.singer||(t.singer="");
}
t.music_name=l.encodeStr(e.getAttribute("music_name")||"").replace(/^\s/,"").replace(/\s$/,""),
p.adapter[t.musictype]&&"function"==typeof p.adapter[t.musictype].initData&&(t=p.adapter[t.musictype].initData(t,{
scene:0
})),l.renderPlayer(m,t,e);
var u=t.musicid+"_"+t.posIndex,c=e.parentNode.querySelector('[data-preloadingid="'+u+'"]');
c&&c.parentNode.removeChild(c),n(t),p.musicList[t.musicid+"_"+t.posIndex]=t;
}
function n(e){
var t=e.musicid+"_"+e.posIndex;
c("[Music] init "+e.detailUrl);
var i=l.decodeStr(e.music_name);
e.player=l.init({
allowPause:e.allowPause===!0?!0:!1,
wxIndex:e.posIndex,
type:e.type||0,
comment_id:"",
mid:e.media_id,
otherid:e.otherid,
albumid:e.albumid,
songId:e.musicid,
jumpurlkey:e.jumpurlkey,
duration:e.duration,
title:i,
singer:window.nickname?window.nickname+"推荐的歌":"公众号推荐的歌",
epname:"音乐",
coverImgUrl:e.albumurl,
playingCss:"qqmusic_playing",
pauseCss:e.pauseCss||"",
playCssDom:u("qqmusic_main_"+t),
playArea:u("qqmusic_play_"+t),
detailUrl:e.detailUrl||"",
webUrl:e.webUrl||"",
detailArea:u("qqmusic_home_"+t)
});
}
function u(e){
return document.getElementById(e);
}
e("biz_common/utils/string/html.js");
var a=e("biz_common/utils/url/parse.js"),c=e("appmsg/log.js"),m=e("pages/qqmusic_tpl.html.js"),l=e("pages/voice_component.js"),p={
adapter:{
1:e("pages/qqmusic_ctrl.js"),
2:e("pages/kugoumusic_ctrl.js")
},
musicList:{},
musicLen:0
};
return t()?(i(),s(),p.musicList):void 0;
});define("appmsg/iframe.js",["biz_common/utils/string/html.js","pages/video_communicate_adaptor.js","biz_wap/utils/mmversion.js","biz_wap/utils/ajax.js","common/utils.js","appmsg/finance_communicate.js","biz_wap/utils/jsmonitor_report.js","biz_common/utils/url/parse.js","new_video/ctl.js","pages/version4video.js","biz_common/dom/attr.js","biz_common/dom/event.js"],function(e){
"use strict";
function t(e){
console.info("iframe_onload");
var t=0;
try{
e.contentDocument&&e.contentDocument.body.offsetHeight?t=e.contentDocument.body.offsetHeight:e.Document&&e.Document.body&&e.Document.body.scrollHeight?t=e.Document.body.scrollHeight:e.document&&e.document.body&&e.document.body.scrollHeight&&(t=e.document.body.scrollHeight);
var i=e.parentElement;
if(i&&(e.style.height=t+"px"),/MSIE\s(7|8)/.test(navigator.userAgent)&&e.contentWindow&&e.contentWindow.document){
var o=e.contentWindow.document.getElementsByTagName("html");
o&&o.length&&(o[0].style.overflow="hidden");
}
s&&s.postPageHeightMessage&&s.postPageHeightMessage("updatePageHeight"),console.log("financeUtils done");
}catch(n){}
}
function i(){
for(var e=window.pageYOffset||document.documentElement.scrollTop,t=p.video_top.length,n=e+r.getInnerHeight(),d=0,s=0;t>s;s++){
var c=p.video_top[s];
c.reported?d++:n>=c.start&&n<=c.end&&(c.reported=!0,setTimeout(function(e,t,i){
return function(){
var n=o.getVideoInfo(),d="",r="",s=3;
n[e]&&(n[e].hit_bizuin&&(d=n[e].hit_bizuin),n[e].hit_vid&&(r=n[e].hit_vid),n[e].ori_status&&(s=n[e].ori_status)),
m.report({
step:1,
hit_vid:r,
hit_bizuin:d,
ori_status:s,
vid:e,
screen_num:Math.ceil(t/i),
screen_height:i
});
};
}(c.vid,n,r.getInnerHeight()),1e4));
}
d==t&&(u.off(window,"scroll",i),p.video_top=p.video_iframe=i=null);
}
e("biz_common/utils/string/html.js");
{
var o=e("pages/video_communicate_adaptor.js"),n=e("biz_wap/utils/mmversion.js"),d=e("biz_wap/utils/ajax.js"),r=e("common/utils.js"),s=e("appmsg/finance_communicate.js"),c=e("biz_wap/utils/jsmonitor_report.js"),a=e("biz_common/utils/url/parse.js"),m=e("new_video/ctl.js"),p={
txVideoReg:/^http(s)*\:\/\/v\.qq\.com\/iframe\/(preview|player)\.html\?/,
mpVideoReg:/^http(s)*\:\/\/mp\.weixin\.qq\.com\/mp\/readtemplate\?t=pages\/video_player_tmpl/,
video_iframe:[],
video_top:[]
},_=e("pages/version4video.js"),l=e("biz_common/dom/attr.js"),u=(l.setProperty,e("biz_common/dom/event.js")),w=document.getElementsByTagName("iframe"),f=[];
/MicroMessenger/.test(navigator.userAgent);
}
window.reportVid=[];
for(var g=Math.ceil(1e4*Math.random()),v=0,h=w.length;h>v;++v)!function(e){
var i=e.getAttribute("data-src")||"",o=e.className||"",r=e.getAttribute("src")||i;
if(!i||"#"==i){
var s=e.getAttribute("data-display-src");
if(s&&(0==s.indexOf("/cgi-bin/readtemplate?t=vote/vote-new_tmpl")||0==s.indexOf("https://mp.weixin.qq.com/cgi-bin/readtemplate?t=vote/vote-new_tmpl"))){
s=s.replace(/&amp;/g,"&");
for(var m=s.split("&"),l=["/mp/newappmsgvote?action=show"],u=0;u<m.length;u++)(0==m[u].indexOf("__biz=")||0==m[u].indexOf("supervoteid="))&&l.push(m[u]);
l.length>1&&(i=l.join("&")+"#wechat_redirect");
}
}
if(r&&(p.txVideoReg.test(r)||p.mpVideoReg.test(r))){
if(_.isShowMpVideo()||p.mpVideoReg.test(r)){
var w=a.getQuery("vid",i);
if(!w)return;
var v=e.getAttribute("data-vw"),h=e.getAttribute("data-vh"),x=document.domain;
"qq.com"==x&&((new Image).src="https://badjs.weixinbridge.com/badjs?id=139&level=4&from="+window.encodeURIComponent(window.location.host)+"&msg="+window.encodeURIComponent(window.location.href),
c.setLogs({
id:27302,
key:100,
value:1,
lc:1,
log0:"[beforeD]"+window.encodeURIComponent(window.location.href)
})),window.reportVid.push(w),p.video_iframe.push({
dom:e,
vid:w
}),r=["/mp/videoplayer?video_h=",h,"&video_w=",v,"&scene=",window.source,"&random_num=",g,"&article_title=",encodeURIComponent(window.msg_title.htmlDecode()),"&source=4&vid=",w,"&mid=",appmsgid,"&idx=",itemidx||idx,"&__biz=",biz,"&nodetailbar=",window.is_temp_url?1:0,"&uin=",uin,"&key=",key,"&pass_ticket=",pass_ticket,"&version=",version,"&devicetype=",window.devicetype||"","&wxtoken=",window.wxtoken||"","&sessionid=",window.sessionid||"","&preview=",window.is_temp_url?1:0,"&is_in_pay_subscribe=",window.isPaySubscribe].join(""),
uin||window.__addIdKeyReport&&window.__addIdKeyReport("28307",21),window.__addIdKeyReport&&window.__addIdKeyReport("28307",11),
setTimeout(function(e,t){
if(t.setAttribute("marginWidth",0),t.setAttribute("marginHeight",0),t.style.top="0",
window.__second_open__)if(n.isIOS){
var i,o,r;
!function(){
var n=function(e,t,i,o){
i&&o&&(e.contentWindow.is_login=t.is_login,e.contentWindow.user_uin=t.user_uin,e.contentWindow.cgiData.ckey=t.ckey,
e.contentWindow.cgiData.ckey_ad=t.ckey_ad,e.contentWindow.seajs.use("pages/video_appmsg.js"));
};
window.__videohook__=1,i=!1,o=!1,r={},t.onload=function(){
console.log("4",Date.now()),i=!0,n(t,r,i,o);
},t.setAttribute("src",e),d({
url:e,
type:"GET",
f:"json",
success:function(d){
o=!0;
try{
r=JSON.parse(d),n(t,r,i,o);
}catch(s){
n(t,r,i,o);
}
window.resp=d,t.setAttribute("data-realsrc",e),t.contentWindow.__iframe_src__=e;
}
});
}();
}else d({
url:e,
type:"GET",
f:"html",
success:function(i){
t.setAttribute("data-realsrc",e),t.contentDocument.open("text/html","replace"),t.contentDocument.write(i),
t.contentDocument.close(),t.contentWindow.__iframe_src__=e,t.contentWindow.history.replaceState(null,null,e);
}
});else t.setAttribute("src",e);
},0,r,e);
}
}else if(i&&(i.indexOf("newappmsgvote")>-1&&(o.indexOf("js_editor_vote_card")>=0||o.indexOf("vote_iframe")>=0)||0==i.indexOf("http://mp.weixin.qq.com/bizmall/appmsgcard")&&(o.indexOf("card_iframe")>=0||o.indexOf("js_editor_card")>=0)||i.indexOf("appmsgvote")>-1||i.indexOf("mp.weixin.qq.com/mp/getcdnvideourl")>-1)){
if(window.is_transfer_msg&&!window.reprint_ticket&&i.indexOf(window.biz)<0)return void f.push(e);
if(window.__second_open__||(i=i.replace(/^http:/,location.protocol)),o.indexOf("card_iframe")>=0||o.indexOf("js_editor_card")>=0){
-1===o.indexOf("card_iframe")&&(e.className+=" card_iframe"),-1===o.indexOf("res_iframe")&&(e.className+=" res_iframe");
var b=i.replace("#wechat_redirect",["&pass_ticket=",pass_ticket,"&scene=",source,"&msgid=",appmsgid,"&msgidx=",itemidx||idx,"&version=",version,"&devicetype=",window.devicetype||"","&child_biz=",biz,"&wxtoken=",window.wxtoken||""].join(""));
reprint_ticket&&(b+=["&mid=",mid,"&idx=",idx,"&reprint_ticket=",reprint_ticket,"&source_mid=",source_mid,"&source_idx=",source_idx].join("")),
window.__second_open__?d({
url:b,
type:"GET",
f:"html",
success:function(o){
e.setAttribute("src",b),e.contentWindow.document.open("text/html","replace"),e.contentWindow.document.write(o),
e.contentWindow.document.close(),e.contentWindow.history.replaceState(null,null,b),
-1==i.indexOf("mp.weixin.qq.com/mp/getcdnvideourl")&&(e.onload=function(){
t(e);
});
}
}):(e.setAttribute("src",b),-1==i.indexOf("mp.weixin.qq.com/mp/getcdnvideourl")&&(e.onload=function(){
t(e);
}));
}else{
var y=i.indexOf("#wechat_redirect")>-1,j=["&uin=",uin,"&key=",key,"&pass_ticket=",pass_ticket,"&wxtoken=",window.wxtoken||""].join("");
reprint_ticket?j+=["&mid=",mid,"&idx=",idx,"&reprint_ticket=",reprint_ticket,"&source_mid=",source_mid,"&source_idx=",source_idx,"&appmsg_token=",appmsg_token].join(""):(o.indexOf("vote_iframe")>=0||o.indexOf("js_editor_vote_card")>=0)&&(j+=["&mid=",mid,"&idx=",idx,"&appmsg_token=",appmsg_token].join(""),
-1===o.indexOf("vote_iframe")&&(e.className+=" vote_iframe"));
var b=y?i.replace("#wechat_redirect",j):i+j;
window.__second_open__?d({
url:b,
type:"GET",
f:"html",
success:function(o){
e.contentWindow.Ajax=d,e.setAttribute("src",b),e.contentWindow.document.open("text/html","replace"),
e.contentWindow.document.write(o),e.contentWindow.document.close(),e.contentWindow.history.replaceState(null,null,b),
-1==i.indexOf("mp.weixin.qq.com/mp/getcdnvideourl")&&(e.onload=function(){
t(e);
});
}
}):(e.setAttribute("src",b),-1==i.indexOf("mp.weixin.qq.com/mp/getcdnvideourl")&&(e.onload=function(){
t(e);
}));
}
e.appmsg_idx=u;
}
if(i&&i.indexOf("mp.weixin.qq.com/mp/getcdnvideourl")>-1&&v>0){
var k=v,O=3*k/4;
e.width=k,e.height=O,e.style.setProperty&&(e.style.setProperty("width",k+"px","important"),
e.style.setProperty("height",O+"px","important"));
}
}(w[v]);
for(var x=0;x<f.length;x++){
var b=f[x];
b.parentNode.removeChild(b);
}
if(window.iframe_reload=function(){
for(var e=0,i=w.length;i>e;++e){
var o=w[e],n=o.getAttribute("src");
n&&(n.indexOf("newappmsgvote")>-1||n.indexOf("appmsgvote")>-1)&&t(o);
}
},"getElementsByClassName"in document)for(var y,j=document.getElementsByClassName("video_iframe"),v=0;y=j.item(v++);)y.setAttribute("scrolling","no"),
y.style.overflow="hidden";
p.video_iframe.length>0&&setTimeout(function(){
for(var e=p.video_iframe,t=document.getElementById("js_article"),o=0,n=e.length;n>o;o++){
var d=e[o];
if(!d||!d.dom)return;
for(var s=d.dom,c=s.offsetHeight,a=0;s&&t!==s;)a+=s.offsetTop,s=s.offsetParent;
p.video_top.push({
start:a+c/2,
end:a+c/2+r.getInnerHeight(),
reported:!1,
vid:d.vid
});
}
i(),u.on(window,"scroll",i);
});
});define("appmsg/page_pos.js",["biz_common/utils/string/html.js","biz_common/dom/event.js","biz_wap/utils/ajax.js","biz_common/utils/cookie.js","biz_common/utils/http.js","appmsg/cdn_img_lib.js","biz_wap/utils/storage.js","biz_wap/utils/hand_up_state.js","biz_wap/utils/mmversion.js","biz_wap/jsapi/core.js","biz_wap/jsapi/leaveReport.js","biz_wap/utils/wapsdk.js","common/utils.js","appmsg/log.js","biz_common/utils/url/parse.js","biz_wap/utils/jsmonitor_report.js"],function(e){
"use strict";
function t(e){
window.logs||(window.logs={}),T.js_content=e.js_content||document.getElementById("js_content");
var t=e.js_toobar3||document.getElementById("js_toobar3");
T.pageEndTop=t?t.offsetTop:0,T.imgs=T.js_content?T.js_content.getElementsByTagName("img")||[]:[],
T.media=e.media||document.getElementById("media"),T.title=e.title||(window.msg_title||"").htmlDecode(),
T.video_cnt=e.video_cnt||window.logs.video_cnt||0,T.js_cmt_area=e.js_cmt_area||document.getElementById("js_cmt_area"),
T.item_show_type=e.item_show_type||window.item_show_type||0,j=document.getElementsByTagName("html"),
j&&1==!!j.length&&l&&(j=j[0].innerHTML,I.content_length=l.htmlSize),window.logs.pageinfo=I,
function(){
if(window.localStorage&&!localStorage.getItem("clear_page_pos")){
for(var e=localStorage.length-1;e>=0;){
var t=localStorage.key(e);
t.match(/^\d+$/)?localStorage.removeItem(t):t.match(/^adinfo_/)&&localStorage.removeItem(t),
e--;
}
localStorage.setItem("clear_page_pos","true");
}
}(),window.localStorage&&(m.on(window,"load",function(){
if(N=1*z.get(B),!window.__second_open__){
var t=location.href.indexOf("scrolltodown")>-1,o=T.js_cmt_area;
if(t&&o&&o.offsetTop){
var i=o.offsetTop;
!e.disableScroll&&window.scrollTo(0,i-25);
}else!e.disableScroll&&window.scrollTo(0,N),f.saveSpeeds({
uin:uin,
pid:"https:"==x?462:417,
speeds:{
sid:36,
time:Math.ceil(N/v.getInnerHeight())
}
}),f.send();
}
if(window.__wxjs_is_wkwebview||window.__second_open__){
if(M)return;
var n=S.getData(),p=localStorage.getItem("hand_up_id");
for(var m in n)m!=p&&n[m]&&(s(n[m].val),y.setSum(28307,59,1),S.remove(m));
window.setInterval(function(){
var e=a();
S.set(P,e,+new Date+864e7);
},1e3);
}
var l=A.getData("spad");
l&&l.spad&&d(l.spad.val),e.hasSpAd&&window.setInterval(function(){
r();
var e=_();
A.set("spad",e,+new Date+864e7);
},1e3),window.setTimeout(function(){
w({
url:"/mp/appmsgreport?action=page_time_5s&__biz="+biz,
type:"POST",
mayAbort:!0,
data:a(),
async:!0,
timeout:2e3
});
},5e3);
}),m.on(window,"unload",function(){
if(b("[Appmsg leaveReport in page_pos 3]"),console.log("[Appmsg leaveReport in page_pos 3]"),
!window.__second_open__&&(b("[Appmsg leaveReport in page_pos 4]"),console.log("[Appmsg leaveReport in page_pos 4]"),
!window.__jsapi_report_has_done__)){
b("[Appmsg leaveReport in page_pos 5]"),console.log("[Appmsg leaveReport in page_pos 5]"),
localStorage.setItem("hand_up_id",""),window.__ajaxtest="2";
var e=a();
s(e),window.__unload_has_done__=!0;
}
}),window.logs.read_height=0,m.on(window,"scroll",function(){
var e=window.pageYOffset||document.documentElement.scrollTop;
window.logs.read_height=Math.max(window.logs.read_height,e),clearTimeout(D),D=setTimeout(function(){
N=window.pageYOffset,z.set(B,N,+new Date+72e5);
},500);
}),m.on(document,"touchmove",function(){
var e=window.pageYOffset||document.documentElement.scrollTop;
window.logs.read_height=Math.max(window.logs.read_height,e),clearTimeout(D),D=setTimeout(function(){
N=window.pageYOffset,z.set(B,N,+new Date+72e5);
},500);
})),h.addReport(function(){
if(b("[Appmsg leaveReport in page_pos 1]"),console.log("[Appmsg leaveReport in page_pos 1]"),
!window.__unload_has_done__){
b("[Appmsg leaveReport in page_pos 2]"),console.log("[Appmsg leaveReport in page_pos 2]"),
k=!0,S.remove(P);
var e=a(),t=[];
for(var o in e)e.hasOwnProperty(o)&&t.push(o+"="+encodeURIComponent(e[o]));
var i={
reportUrl:"https://mp.weixin.qq.com/mp/appmsgreport?action=page_time&__biz="+biz,
reportData:t.join("&"),
method:"POST"
};
return window.__jsapi_report_has_done__=!0,b("[Appmsg leaveReport length]: "+JSON.stringify(i).length),
console.log("[Appmsg leaveReport length]: "+JSON.stringify(i).length),i;
}
}),m.on(document,"visibilitychange",function(){
g.isHidden()?localStorage.setItem("hand_up_id",P):localStorage.setItem("hand_up_id","");
}),p();
}
function o(e,t){
if(e&&!(e.length<=0))for(var o,i,n,a=/http(s)?\:\/\/([^\/\?]*)(\?|\/)?/,s=0,r=e.length;r>s;++s)o=e[s],
o&&(i=o.getAttribute(t),i&&(n=i.match(a),n&&n[2]&&(O[n[2]]=!0)));
}
function i(e){
for(var t=0,o=R.length;o>t;++t)if(R[t]==e)return!0;
return!1;
}
function n(){
O={},o(document.getElementsByTagName("a"),"href"),o(document.getElementsByTagName("link"),"href"),
o(document.getElementsByTagName("iframe"),"src"),o(document.getElementsByTagName("script"),"src"),
o(document.getElementsByTagName("img"),"src");
var e=[];
for(var t in O)O.hasOwnProperty(t)&&(window.networkType&&"wifi"==window.networkType&&!E&&i(t)&&(E=!0),
e.push(t));
return O={},e.join(",");
}
function a(){
{
var e,t=window.pageYOffset||document.documentElement.scrollTop,o=T.js_content,i=v.getInnerHeight(),a=T.screen_width,s=T.scroll_height,r=Math.ceil(s/i),_=Math.ceil((o.scrollHeight||o.offsetHeight)/i),d=(window.logs.read_height||t)+i,p=T.pageEndTop,m=T.imgs,w=Math.ceil(d/i)||1,l=T.media,c=50,u=0,h=0,f=0,b=0,y=d+c>p?1:0;
o.offsetTop+o.scrollHeight;
}
w>r&&(w=r);
var z=function(t){
if(t)for(var o=0,i=t.length;i>o;++o){
var n=t[o];
if(n){
u++;
var a=n.getAttribute("src"),s=n.getAttribute("data-type");
a&&0==a.indexOf("http")&&(h++,a.isCDN()&&(f++,-1!=a.indexOf("tp=webp")&&b++),s&&(e["img_"+s+"_cnt"]=e["img_"+s+"_cnt"]||0,
e["img_"+s+"_cnt"]++));
}
}
e.download_cdn_webp_img_cnt=b||0,e.download_img_cnt=h||0,e.download_cdn_img_cnt=f||0,
e.img_cnt=u||0;
},S=window.appmsgstat||{},A=window.logs.img||{},O=window.logs.pagetime||{},x=A.load||{},R=A.read||{},k=[],D=[],N=0,B=0,H=0;
for(var P in R)P&&0==P.indexOf("http")&&R.hasOwnProperty(P)&&D.push(P);
for(var P in x)P&&0==P.indexOf("http")&&x.hasOwnProperty(P)&&k.push(P);
for(var M=0,q=k.length;q>M;++M){
var G=k[M];
G&&G.isCDN()&&(-1!=G.indexOf("/0")&&N++,-1!=G.indexOf("/640")&&B++,-1!=G.indexOf("/300")&&H++);
}
var e={
report_bizuin:biz,
title:T.title,
mid:mid,
idx:idx,
subscene:window.subscene||1e4,
sessionid:window.sessionid||0,
read_cnt:S.read_num||0,
like_cnt:S.like_num||0,
screen_width:a,
screen_height:v.getInnerHeight(),
screen_num:_,
idkey:"",
copyright_stat:"",
ori_article_type:"",
video_cnt:T.video_cnt,
read_screen_num:w||0,
is_finished_read:y,
scene:source,
content_len:I.content_length||0,
start_time:page_begintime,
end_time:(new Date).getTime(),
handup_time:g.getHandUpTime(),
total_height:p,
exit_height:d>p?p:d,
img_640_cnt:B,
img_0_cnt:N,
img_300_cnt:H,
wtime:O.onload_time||0,
ftime:O.ftime||0,
ptime:O.ptime||0,
onload_time:O.onload_time||0,
reward_heads_total:window.logs.reward_heads_total||0,
reward_heads_fail:window.logs.reward_heads_fail||0,
outer_pic:window.logs.outer_pic||0,
publish_time:window.ct,
item_show_type:T.item_show_type,
page_req_info:JSON.stringify({
startGetAppmsgExtTime:window.startGetAppmsgExtTime,
startGetAppmsgAdTime:window.startGetAppmsgAdTime,
receiveGetAppmsgExt:window.receiveGetAppmsgExt,
receiveGetAppmsgAd:window.receiveGetAppmsgAd,
jsapiReadyTime:window.jsapiReadyTime,
domCompleteTime:window.domCompleteTime
})
};
if(window.networkType&&"wifi"==window.networkType&&(e.wifi_all_imgs_cnt=k.length,
e.wifi_read_imgs_cnt=D.length),window.logs.webplog&&4==window.logs.webplog.total){
var C=window.logs.webplog;
e.webp_total=1,e.webp_lossy=C.lossy,e.webp_lossless=C.lossless,e.webp_alpha=C.alpha,
e.webp_animation=C.animation;
}
if(e.copyright_stat=window._copyright_stat||"",e.ori_article_type=window._ori_article_type||"",
window.__addIdKeyReport&&window.moon&&(moon.hit_num>0&&moon.hit_num<1e3&&window.__addIdKeyReport(27613,30,moon.hit_num),
moon.mod_num>0&&moon.mod_num<1e3&&window.__addIdKeyReport(27613,31,moon.mod_num)),
window.logs.idkeys){
var Y=window.logs.idkeys,J=[];
for(var K in Y)if(Y.hasOwnProperty(K)){
var U=Y[K];
U.val>0&&J.push(K+"_"+U.val);
}
e.idkey=J.join(";");
}
z(!!l&&l.getElementsByTagName("img")),z(m);
var L=(new Date).getDay(),V=n();
return(E||0!==user_uin&&Math.floor(user_uin/100)%7==L)&&(e.domain_list=V),E&&(e.html_content=j),
window.isSg&&(e.from="sougou"),e.source=window.friend_read_source||"",e.req_id=window.req_id||"",
e.recommend_version=window.friend_read_version||"",e.class_id=window.friend_read_class_id||"",
e.ascene=window.ascene||-1,0==e.scene&&56==e.ascene&&(e.scene=90),e.hotspotjson=JSON.stringify({
hotspotinfolist:window.hotspotInfoList||[]
}),e.is_pay_subscribe=window.isPaySubscribe,e.is_paid=window.isPaid,e.preview_percent=window.previewPercent,
e.is_finished_preview=window.is_finished_preview||0,e.fee=window.paySubscribeInfo?window.paySubscribeInfo.fee:"",
e.pay_cnt=window.paySubscribeInfo?window.paySubscribeInfo.pay_cnt:"",e.worthy_cnt=window.paySubscribeInfo?window.paySubscribeInfo.like_cnt:"",
e;
}
function s(e){
k||(k=!0,S.remove(P),e.report_time=parseInt(+new Date/1e3),w({
url:"/mp/appmsgreport?action=page_time&__biz="+biz,
type:"POST",
mayAbort:!0,
data:e,
async:!1,
timeout:2e3
}));
}
function r(){
z.set(B,N,+new Date+72e5);
}
function _(){
return window.__video_report_data;
}
function d(e){
e&&e.play_type&&(A.remove("spad"),e.report_type=1,w({
url:"/mp/ad_video_report?action=video_play_report",
type:"POST",
mayAbort:!0,
data:e,
async:!1,
timeout:2e3
}));
}
function p(){
(new Image).src=location.protocol+"//mp.weixin.qq.com/mp/geticon?__biz="+biz+"&r="+Math.random();
}
e("biz_common/utils/string/html.js");
var m=e("biz_common/dom/event.js"),w=e("biz_wap/utils/ajax.js"),l=(e("biz_common/utils/cookie.js"),
e("biz_common/utils/http.js"));
e("appmsg/cdn_img_lib.js");
var c=e("biz_wap/utils/storage.js"),g=e("biz_wap/utils/hand_up_state.js"),u=e("biz_wap/utils/mmversion.js"),h=(e("biz_wap/jsapi/core.js"),
e("biz_wap/jsapi/leaveReport.js")),f=e("biz_wap/utils/wapsdk.js"),v=e("common/utils.js"),b=e("appmsg/log.js"),y=(e("biz_common/utils/url/parse.js"),
-1!=navigator.userAgent.indexOf("TBS/"),e("biz_wap/utils/jsmonitor_report.js"));
window.__unload_has_done__=!1;
var j,T={
js_cmt_area:null,
js_content:null,
screen_height:v.getInnerHeight(),
screen_width:document.documentElement.clientWidth||window.innerWidth,
scroll_height:document.body.scrollHeight||document.body.offsetHeight,
pageEndTop:0,
imgs:[],
media:null,
title:"",
video_cnt:0,
item_show_type:0
},z=new c("page_pos"),S=new c("time_on_page"),A=new c("spad"),I={},O={},x=window.location.protocol,E=!1,R=["wap.zjtoolbar.10086.cn","125.88.113.247","115.239.136.61","134.224.117.240","hm.baidu.com","c.cnzz.com","w.cnzz.com","124.232.136.164","img.100msh.net","10.233.12.76","wifi.witown.com","211.137.132.89","qiao.baidu.com","baike.baidu.com"],k=!1,D=null,N=0,B=[biz,sn,mid,idx].join("_"),H=Math.random(),P=[biz,sn,mid,idx,H].join("_"),M=u.isAndroid&&u.gtVersion("7.0.4",!0)||u.isIOS&&u.gtVersion("7.0.4",!0);
return{
init:t
};
});define("appmsg/product.js",["biz_common/dom/event.js","common/utils.js"],function(e){
"use strict";
function t(){
for(var e=window.pageYOffset||document.documentElement.scrollTop,t=0;t<i.length;++t){
var o=i[t];
if(!o.isReport){
var n=o.offsetTop;
n>=e&&e+r.getInnerHeight()>=n&&(o.isReport=!0,(new Image).src="/mp/appmsgreport?action=appmsg_recom&type=1&__biz="+biz+"&ascene="+(window.ascene||-1)+"&mid="+mid+"&idx="+idx+"&sn="+sn+"&product_id="+o.product_id+"&order="+o.order+"&r="+Math.random());
}
}
}
var o=e("biz_common/dom/event.js"),r=e("common/utils.js");
if(document.getElementsByClassName){
for(var n=document.getElementsByClassName("js_product_section"),d=document.getElementsByClassName("js_product_a"),i=[],s=0;s<n.length;++s){
var a=n[s];
a.dataset&&a.dataset.product_id&&a.dataset.order&&i.push({
dom:a,
offsetTop:a.offsetTop,
product_id:a.dataset.product_id||"",
order:a.dataset.order||"",
isReport:!1
});
}
i.length>0&&(o.on(window,"scroll",t),t());
for(var s=0;s<d.length;++s)!function(e){
o.on(e,"click",function(){
var t=e.dataset||{};
return(new Image).src="/mp/appmsgreport?action=appmsg_recom&type=2&__biz="+biz+"&ascene="+(window.ascene||-1)+"&mid="+mid+"&idx="+idx+"&sn="+sn+"&product_id="+(t.product_id||"")+"&order="+(t.order||"")+"&r="+Math.random(),
t.href?(setTimeout(function(){
location.href="http://mp.weixinbridge.com/mp/wapredirect?url="+encodeURIComponent(t.href)+"&action=appmsg_redirect&uin="+uin+"&biz="+biz+"&mid="+mid+"&idx="+idx+"&scene=0";
},300),!1):!1;
},!0);
}(d[s]);
}
});define("appmsg/review_image.js",["biz_common/dom/event.js","biz_wap/jsapi/core.js","biz_common/utils/url/parse.js","appmsg/log.js","biz_wap/utils/ajax.js","biz_wap/utils/mmversion.js","appmsg/cdn_img_lib.js"],function(e){
"use strict";
function t(e,t,o,a){
var i={
current:e,
urls:t,
currentInfo:{
url:e,
data:o,
pos:a
},
forbidForward:window.isPaySubscribe?1:0
};
console.log("imagePreview request",i),console.log("previewFlag",g),g||(g=!0,r.invoke("imagePreview",i,function(e){
console.log("imagePreview response",e),window.__addIdKeyReport&&window.__addIdKeyReport("28307","2");
}),setTimeout(function(){
g=!1;
},500),d("[Appmsg] click image, src: "+e));
}
function o(e,t){
s({
url:"/mp/rewardappmsgreport",
data:{
__biz:window.biz||"",
mid:window.mid||"",
idx:window.idx||"",
oper:t||"",
cdn_url:e||"",
ascene:window.ascene||-1
},
type:"POST",
dataType:"json",
async:!0
});
}
function a(e){
var a=[],r=e.container,d=e.imgs||[];
if(r)for(var s=r.getElementsByTagName("img")||[],g=0,l=s.length;l>g;g++)d.push(s.item(g));
for(var c=p.isIOS&&1==window._copyright_stat&&1==window.is_need_reward,m=0,g=0,l=d.length;l>g;g++){
var w=d[g],u=w.getAttribute("data-src")||w.getAttribute("src"),h=w.getAttribute("data-type");
if(u&&!u.isGif()&&0!=u.indexOf("data:")){
for(;-1!=u.indexOf("?tp=webp");)u=u.replace("?tp=webp","");
w.dataset&&w.dataset.s&&u.isCDN()&&(u=u.replace(/\/640$/,"/0"),u=u.replace(/\/640\?/,"/0?")),
u.isCDN()&&(u=n.addParam(u,"wxfrom","3",!0)),u=e.is_https_res?u.http2https():u.https2http(),
h&&(u=n.addParam(u,"wxtype",h,!0)),a.push(u),"1"!=w.getAttribute("data-nopreviewclick")&&!function(e){
p.isAndroid&&w.setAttribute("data-wxsrc",e),i.on(w,"click",function(i){
if(i.stopPropagation(),!(i&&i.target&&i.target.className&&i.target.className.indexOf("img_loadederror")>-1)){
if("function"==typeof window.__addIdKeyReport&&window.__addIdKeyReport("110644",2),
window.getComputedStyle){
for(var r=i.target,n=r.getBoundingClientRect(),d=.15*n.width,s=.15*n.height,g=!0;r&&"body"!=r.nodeName.toLowerCase();){
var l=window.getComputedStyle(r,null),w=parseInt(l.getPropertyValue("opacity")),u=l.getPropertyValue("filter"),h=l.getPropertyValue("visibility"),f=l.mixBlendMode;
if(1!=w||"visible"!=h||u.indexOf("opacity")>=0||u.indexOf("blur")>=0||f&&"normal"!=f){
g=!1;
break;
}
var b=r.getBoundingClientRect();
if(("hidden"==l.overflow||"hidden"==l.overflowX||"hidden"==l.overflowY)&&(b.left-n.left>d||b.right-n.right<-1*d||b.top-n.top>s||b.bottom-n.bottom<-1*s)){
g=!1;
break;
}
r=r.parentElement;
}
if(!g){
if(console.log("don't try this again"),"function"==typeof window.__addIdKeyReport){
window.__addIdKeyReport("110644",3);
var y=new Image,_="https://badjs.weixinbridge.com/badjs?id=168&level=4&from="+encodeURIComponent(location.href)+"&msg="+encodeURIComponent(e);
y.src=_.slice(0,1024);
}
return!1;
}
}
"undefined"==typeof getComputedStyle&&(window.getComputedStyle=document.body.currentStyle?function(e){
return e.currentStyle;
}:{});
var v=i.target,j=window.getComputedStyle(v),F=v.getBoundingClientRect(),x=document.createElement("canvas");
x.style.width=j.width,x.style.height=j.height,x.width=parseFloat(j.width),x.height=parseFloat(j.height);
var C=x.getContext("2d"),I="";
C.drawImage(v,0,0,parseFloat(j.width),parseFloat(j.height));
try{
I=x.toDataURL();
}catch(i){}
p.isAndroid&&(I=""),t(e,a,I,{
x:F.left-parseFloat(j.paddingLeft)-parseFloat(j.borderLeftWidth),
y:F.top-parseFloat(j.paddingTop)-parseFloat(j.borderTopWidth),
width:F.width-parseFloat(j.paddingLeft)-parseFloat(j.paddingRight)-parseFloat(j.borderLeftWidth)-parseFloat(j.borderRightWidth),
height:F.height-parseFloat(j.paddingTop)-parseFloat(j.paddingBottom)-parseFloat(j.borderTopWidth)-parseFloat(j.borderBottomWidth)
}),c&&0==m&&o(i.target.src,2);
}
});
}(u),w.removeAttribute("data-nopreviewclick");
}
}
if(c){
var f=document.getElementById("js_content"),b=0,y=0;
i.on(f,"touchstart",function(e){
return e&&e.target&&e.target.tagName&&"string"==typeof e.target.tagName&&"IMG"==e.target.tagName.toString().toUpperCase()?(m=+new Date,
b=e.touches[0].pageX,void(y=e.touches[0].pageY)):void(m=0);
}),i.on(f,"touchmove",function(e){
var t=e.touches[0].pageX,o=e.touches[0].pageY;
Math.abs(t-b)>10&&Math.abs(o-y)>10&&(m=0);
}),i.on(f,"touchend",function(e){
0!=m&&(+new Date-m>800&&+new Date-m<6e3?o(e.target.src,1):m=0);
});
}
}
var i=e("biz_common/dom/event.js"),r=e("biz_wap/jsapi/core.js"),n=e("biz_common/utils/url/parse.js"),d=e("appmsg/log.js"),s=e("biz_wap/utils/ajax.js"),p=e("biz_wap/utils/mmversion.js"),g=!1;
return e("appmsg/cdn_img_lib.js"),a;
});define("appmsg/outer_link.js",["biz_common/dom/event.js","appmsg/open_url_with_webview.js","biz_wap/jsapi/core.js","biz_wap/utils/mmversion.js","biz_wap/utils/ajax.js","appmsg/popup_report.js","biz_wap/utils/jsmonitor_report.js"],function(e){
"use strict";
function t(e){
e.preventDefault();
}
function i(e){
var t=e.innerHTML,i=/<img.*src=[\'\"]/,n=/background-image:(\s*)url\(/,o=/background:[^;"']+url\(/;
return i.test(t)||n.test(t)||o.test(t)?!0:!1;
}
function n(e){
var t=e.innerHTML,i=e.style.fontSize;
return 0===t.trim().length||0===parseFloat(i)?!0:!1;
}
function o(e,t){
var i=e.getElementsByClassName("weui-dialog__bd")[0],n=e.getElementsByClassName("weui-dialog")[0];
if(e.getElementsByClassName("weui-dialog__hd")&&e.getElementsByClassName("weui-dialog__hd").length>0&&n.removeChild(e.getElementsByClassName("weui-dialog__hd")[0]),
t.title&&t.desc){
var o=document.createElement("div");
o.setAttribute("class","weui-dialog__hd");
var r='<strong class="weui-dialog__title">'+t.title+"</strong>";
o.innerHTML=r,i.innerText=t.desc,n.insertBefore(o,i);
}else i.innerText=t.desc;
}
function r(e){
var r=e.container;
if(!r)return!1;
for(var _=r.getElementsByTagName("a")||[],j=0,v=_.length;v>j;++j)!function(r){
var j=_[r],v=j.getAttribute("href");
if(!v)return!1;
var b=0,h=j.innerHTML;
/^[^<>]+$/.test(h)?b=1:/^<img[^>]*>$/.test(h)&&(b=2);
var k=j.getAttribute("data-linktype"),E=j.getAttribute("href");
s.on(j,"tap",function(r){
var s=j.getAttribute("href");
if(!s)return!1;
!!e.changeHref&&!/^https?:\/\/mp\.weixin\.qq\.com\/cgi-bin\//.test(s)&&(s=e.changeHref(s,b)),
r.preventDefault();
var _="";
c[j.getAttribute("data-itemshowtype")]&&(_=c[j.getAttribute("data-itemshowtype")]);
document.getElementById("js_link_dialog_name");
return y&&(d[E]&&d[E].subject_name&&"0"===d[E].item_show_type&&d[E].title?o(y,{
title:'即将打开公众号 "'+d[E].subject_name+'" 的'+c[d[E].item_show_type],
desc:w.innerText="《"+d[E].title+"》"
}):d[E]&&d[E].subject_name&&d[E].item_show_type>=0?o(y,{
desc:'即将打开公众号 "'+d[E].subject_name+'" 的'+c[d[E].item_show_type]
}):o(y,{
desc:"即将打开新的页面"
})),r.stopPropagation(),"undefined"==typeof g[E]&&(E.indexOf("mp.weixin.qq.com/s/")>-1||E.indexOf("mp.weixin.qq.com/s?")>-1)?p.setSum(110809,6,1):"undefined"==typeof g[E]&&p.setSum(110809,7,1),
g=function(){
return d[E]&&d[E].item_show_type>=0&&s.indexOf("mp.weixin.qq.com")>-1&&(l.isIOS||l.isAndroid)&&!l.isInMiniProgram&&l.isWechat?1==j.getAttribute("clicked")?!1:(u.invoke("openWebViewUseFastLoad",{
url:s,
item_show_type:d[E].item_show_type,
openType:0,
scene:1
},function(e){
console.log("openWebViewUseFastLoad res: ",e),e&&e.err_msg&&-1==e.err_msg.indexOf("ok")?u.invoke("openUrlWithExtraWebview",{
url:s,
openType:1
},function(e){
j.setAttribute("clicked",0),e&&e.err_msg&&-1==e.err_msg.indexOf("ok")&&(window.location.href=url);
}):(j.setAttribute("clicked",0),p.setSum(28839,37,1));
}),!1):void(l.isInMiniProgram?location.href=s:(l.isAndroid||l.isIOS)&&l.isWechat?a(s,{
sample:1,
reject:function(){
location.href=s;
}
}):location.href=s);
},("1"===k||i(j)||n(j))&&m.report([2,m.getRedirectType(E),"",f?1:0,window.source,m.getUrlData(E)]),
("1"===k||i(j)||n(j))&&f?(console.log("tap img link"),y.style.display="block",y._url=E,
(i(j)||n(j))&&(p.setSum(110809,8,1),y._type="OTHER"),document.querySelector("body").addEventListener("touchmove",t,{
passive:!1
})):g(),!1;
},!0),s.on(j,"click",function(e){
("1"===k||"2"===k||i(j)||n(j))&&f&&(e.preventDefault(),e.stopPropagation());
},!0);
}(j);
}
var s=e("biz_common/dom/event.js"),a=e("appmsg/open_url_with_webview.js"),u=e("biz_wap/jsapi/core.js"),l=e("biz_wap/utils/mmversion.js"),m=(e("biz_wap/utils/ajax.js"),
e("appmsg/popup_report.js")),p=e("biz_wap/utils/jsmonitor_report.js"),c={
0:"文章",
11:"文章",
8:"图片",
7:"语音",
5:"视频"
},d={};
if("undefined"!=typeof jumpInfo)for(var _=0;_<jumpInfo.length;_++)d[jumpInfo[_].url]={
title:jumpInfo[_].title,
item_show_type:jumpInfo[_].item_show_type,
subject_name:jumpInfo[_].subject_name,
link_type:jumpInfo[_].link_type
};
var g=function(){},f=window.img_popup,y=document.getElementById("js_link_dialog"),w=(document.getElementById("js_link_dialog_head"),
document.getElementById("js_link_dialog_body"));
return s.on(document.getElementById("js_link_dialog_ok"),"tap",function(e){
e.stopPropagation(),e.preventDefault(),"OTHER"===y._type&&p.setSum(110809,10,1),
m.report([4,m.getRedirectType(y._url),"",f?1:0,window.source,m.getUrlData(y._url)]),
document.querySelector("body").removeEventListener("touchmove",t),g&&g(),y.style.display="none";
}),s.on(document.getElementById("js_link_dialog_cancel"),"tap",function(e){
e.stopPropagation(),e.preventDefault(),document.querySelector("body").removeEventListener("touchmove",t),
"OTHER"===y._type&&p.setSum(110809,9,1),y.style.display="none",m.report([3,m.getRedirectType(y._url),"",f?1:0,window.source,m.getUrlData(y._url)]);
}),r;
});define("appmsg/copyright_report.js",["common/utils.js","biz_common/dom/event.js"],function(o){
"use strict";
function i(o){
var i=["/mp/copyrightreport?action=report&biz=",biz,"&scene=",o.scene,"&user_uin=",user_uin,"&uin=",uin,"&key=",key,"&pass_ticket=",pass_ticket,"&mid=",window.mid,"&idx=",window.idx,"&source_biz=",window.source_biz,"&source_mid=",window.source_mid,"&source_idx=",window.source_idx,"&card_version=2","&show_appmsg_scene=",window.source,"&session_id=",window.sessionid,"&has_recommend_msg=",window.hasRecommendMsg,"&t=",Math.random()].join("");
window.isSg&&(i+="&from=sougou");
var e=new Image;
e.src=i.substr(0,1024);
}
function e(){
var o=__appmsgCgiData;
if("2"==o.copyright_stat){
for(var i=r("copyright_info"),e=r("js_article");i&&e!==i;)c.copyright_top+=i.offsetTop,
i=i.offsetParent;
t.on(window,"scroll",n),n();
}
}
function n(){
var o=window.pageYOffset||document.documentElement.scrollTop;
o+s.getInnerHeight()>c.copyright_top&&(i({
scene:"1",
card_pos:"0"
}),t.off(window,"scroll",n),n=c.copyright_top=null);
}
function r(o){
return document.getElementById(o);
}
var s=o("common/utils.js"),t=o("biz_common/dom/event.js"),c={
copyright_top:0
};
return{
card_click_report:i,
card_pv_report:e
};
});var _extends=Object.assign||function(e){
for(var t=1;t<arguments.length;t++){
var i=arguments[t];
for(var a in i)Object.prototype.hasOwnProperty.call(i,a)&&(e[a]=i[a]);
}
return e;
};
define("appmsg/async.js",["biz_wap/ui/weui.js","biz_common/utils/string/html.js","appmsg/reward_utils.js","appmsg/pay_read_utils.js","appmsg/pay_report_utils.js","pages/create_txv.js","pages/video_ctrl.js","biz_common/utils/url/parse.js","appmsg/img_copyright_tpl.html.js","appmsg/appmsgext.js","appmsg/share_tpl.html.js","biz_common/dom/event.js","biz_wap/utils/ajax.js","biz_wap/jsapi/core.js","biz_common/tmpl.js","complain/localstorage.js","appmsg/log.js","rt/appmsg/getappmsgext.rt.js","a/a_utils.js","appmsg/related_article.js","appmsg/set_font_size.js","biz_wap/utils/device.js","biz_wap/utils/mmversion.js","pages/version4video.js","appmsg/like.js","appmsg/comment.js","appmsg/iframe.js","redpackage/redpacketcover.js","appmsg/more_read.js"],function(e){
"use strict";
function t(){
for(var t=document.getElementsByTagName("iframe"),a=[],r=0,n=t.length;n>r;++r)a.push(t[r]);
t=null;
var o=document.getElementById("js_content"),s=o.offsetWidth,d=s/m.getRatio();
window.logs.video_cnt=0;
for(var r=0,n=a.length;n>r;++r){
var _=a[r],c=_.getAttribute("data-src")||"",p=_.getAttribute("src")||c;
if(p){
var l=e("pages/version4video.js");
if(0==p.indexOf("http://z.weishi.com/weixin/player.html"))p=p.replace(/width=\d+/g,"width="+s),
p=p.replace(/height=\d+/g,"height="+d),_.width=s,_.height=d,_.style.setProperty&&(_.style.setProperty("width",s+"px","important"),
_.style.setProperty("height",d+"px","important")),_.setAttribute("src",p),window.__addIdKeyReport&&window.__addIdKeyReport("28307",10),
window.logs.video_cnt++;else{
if(/http(s)*\:\/\/v\.qq\.com\/iframe\/(preview|player)\.html\?/.test(p)){
if(!l.isShowMpVideo()){
var w;
w=i(h?_:_),w&&x.push(w),"function"==typeof window.__addIdKeyReport&&(window.__addIdKeyReport("28307",10),
l.device.inWechat&&l.device.inWindowWechat?window.__addIdKeyReport("110644",0):l.device.inWechat&&l.device.inMacWechat&&window.__addIdKeyReport("110644",1));
}
window.logs.video_cnt++;
continue;
}
/^http(s)*\:\/\/mp\.weixin\.qq\.com\/mp\/readtemplate\?t=pages\/video_player_tmpl/.test(p)&&window.logs.video_cnt++;
}
}
}
x.length>0&&"function"==typeof window.__getVideoWh&&y.on(window,"resize",function(){
try{
for(var e=0,t=x.length;t>e;e++){
var i=x[e],a=i.playerObj;
if(a){
var r=window.__getVideoWh(i);
i.style.width=r.w+"px",i.style.height=r.h+"px",a.resize({
width:r.vw,
height:r.vh
});
}
}
}catch(n){}
},!1);
}
function i(e){
var t=e.getAttribute("data-src")||e.getAttribute("src"),i=p.getQuery("vid",t),r=e.getAttribute("data-vw"),n=e.getAttribute("data-vh"),o=e.getAttribute("data-ratio"),s=document.createElement("span");
s.setAttribute("data-ratio",o),s.id="js_tx_video_container_"+Math.random(),s.className="js_tx_video_container",
s.style.cssText=e.style.cssText,s.style.display="none";
var d=e.parentNode;
return d?(d.lastChild===e?d.appendChild(s):d.insertBefore(s,e.nextSibling),c.createTxVideo({
containerId:s.id,
vid:i,
width:r,
height:n,
autoplay:!1,
allowFullScreen:!0,
onSuccess:function(e){
s.playerObj=e.player,a(s,i),s.style.display="block";
},
onError:function(){}
}),d.removeChild(e),s):void 0;
}
function a(e,t){
if(t&&e){
var i=e.parentNode;
if(i){
for(var a=[],r=0,n=i.children.length;n>r;r++){
var o=i.children[r];
o.className.indexOf("img_loading")>=0&&o.getAttribute("data-vid")==t&&a.push(o);
}
for(var r=0,n=a.length;n>r;r++)i.removeChild(a[r]);
e.style.display="block";
}
}
}
function r(e){
if(e&&e.img_copy_info&&e.img_copy_info.list){
for(var t={},i=e.img_copy_info.list,a=window.__appmsgCgiData.copyright_stat,r=window.__appmsgCgiData.source_biz,n=0,o=i.length;o>n;n++){
var s=i[n];
if(2==s.type){
if(2==a&&r==s.source_uin)continue;
t[s.img_url]={
source_nickname:s.source_nickname,
source_uin:s.source_uin,
source_encode_biz:s.source_encode_biz||""
};
}
}
for(var d=document.getElementsByTagName("img"),n=0,o=d.length;o>n;n++){
var s=d[n],_=s.getAttribute("data-src")||s.getAttribute("data-backsrc")||"";
if(t[_]){
var c=document.createElement("div");
c.innerHTML=b.tmpl(l,t[_]);
{
var m=c.children[0],p=s.parentNode,w=p.insertBefore(m,s),u=w.children[0];
(function(e,t){
y.on(t,"click",function(){
var t="https://mp.weixin.qq.com/mp/profile_ext?action=home&__biz="+e.source_encode_biz+"&scene=112#wechat_redirect";
return-1!=navigator.userAgent.indexOf("WindowsWechat")||-1!=navigator.userAgent.indexOf("Mac OS")?(location.href=t,
!1):(f.invoke("openUrlWithExtraWebview",{
url:t,
openType:1
},function(e){
-1==e.err_msg.indexOf("ok")&&(location.href=t);
}),!1);
});
})(t[_],u);
}
w.insertBefore(s,u);
}
}
}
}
function n(t){
var i=t.appmsgstat||{},a=t.paySubscribeInfo||{};
if(window.paySubscribeInfo=a,window.isFans=t.is_fans,window.appmsgstat||(window.appmsgstat=i),
i.show){
{
var r=document.getElementById("js_read_area3"),n=document.getElementById("like3"),o=document.getElementById("like_old"),_=document.getElementById("likeNum3"),c=document.getElementById("likeNum_old"),m=document.getElementById("readNum3");
document.getElementById("js_like_title");
}
if(!(r&&n&&_&&m))return;
var p,l,w=e("appmsg/like.js");
if(1==appmsg_like_type?(p=o,l=c):(p=n,l=_),i.liked=window.is_temp_url?window.liked:i.liked,
w.showReadNum({
show:!0,
readAreaDom:r,
readNumDom:m,
readAreaDisplayValue:window.isPaySubscribe?"none":"block",
readNum:window.is_temp_url?window.read_num:i.read_num
}),f.invoke("handleHaokanAction",{
imgUrl:ori_head_img_url?ori_head_img_url:"",
link:msg_link.html(!1),
desc:msg_desc?msg_desc:"",
title:msg_title?msg_title.htmlDecode():"",
action:"update_recommend_status",
permission:i.like_disabled||2!==appmsg_like_type?0:1,
recommend:i.liked?1:0
},function(){}),!i.like_disabled){
var g=1===appmsg_like_type?"praised":"like_btn_liked";
w.showLikeNum({
show:!0,
likeAreaDom:p,
likeNumDom:l,
liked:i.liked,
className:g,
likeAreaDisplayValue:"inline",
likeNum:window.is_temp_url?window.like_num:i.like_num
}),w.initLikeEvent({
likeAreaDom:p,
likeNumDom:l,
className:g,
prompted:i.prompted,
biz:window.biz,
mid:window.mid,
idx:window.idx,
appmsgid:window.appmsgid,
itemidx:window.itemidx,
is_temp_url:window.is_temp_url,
showType:i.style
});
}
}
var h=document.getElementById("js_share_appmsg");
t.share_redirect_url&&h&&(window._share_redirect_url=t.share_redirect_url,h.innerHTML=b.tmpl(u,{
url:t.share_redirect_url
})),1===t.comment_enabled&&!function(){
var i=e("appmsg/comment.js");
(!window.isPaySubscribe||window.isPaySubscribe&&window.isPaid)&&hasRelatedArticleInfo&&!A?E=function(e){
return function(){
i.initComment(e);
};
}(t):i.initComment(t);
}(),j.setBackgroundClass(),s.init(_extends({
isFans:t.is_fans
},t.reward),{
reward_entrance_enable_for_preview:t.reward_entrance_enable_for_preview,
reward_wording:t.reward_wording,
reward_author_head:t.reward_author_head
}),window.isPaySubscribe&&d.init(a,{
rewardTotal:t.reward.reward_total||0,
rewardTotalCut:t.reward.is_reward_total_count_cut
});
var v=document.getElementById("js_cmt_container");
if(1==t.comment_entrance_enable_for_preview&&window.is_temp_url&&v&&(v.style.display="block"),
t.comment_entrance_enable_for_preview&&(document.getElementById("js_preview_cmt")&&(document.getElementById("js_preview_cmt").style.display="block"),
y.on(document.getElementById("js_preview_cmt_write"),"tap",function(e){
e.preventDefault(),window.weui.alert("预览状态下无法操作");
})),t.comment_enabled&&v&&(v.style.display="block"),S.isIOS&&"block"===v.style.display&&location.href.match(/fontScale=\d+/)&&I.os.ipad&&I.os.getNumVersion()>=13){
var k=location.href.match(/fontScale=(\d+)/);
z(v,parseFloat(k[1])/100);
}
}
function o(){
var t=0,i="27613",a="50";
w.getData({
biz:biz,
appmsg_type:appmsg_type,
mid:mid,
sn:sn,
idx:idx,
scene:source,
title:msg_title,
ct:ct,
abtest_cookie:abtest_cookie,
devicetype:devicetype,
version:window.clientversion,
is_need_ticket:x&&x.length>0?1:0,
is_need_ad:0,
comment_id:comment_id,
is_need_reward:is_need_reward,
both_ad:0,
reward_uin_count:is_need_reward?3*s.getCountPerLine({
can_reward:!0
})-1:0,
send_time:window.send_time||"",
msg_daily_idx:msg_daily_idx,
item_show_type:window.item_show_type,
is_original:t,
is_only_read:is_only_read,
req_id:window.req_id||"",
pass_ticket:pass_ticket,
is_temp_url:window.is_temp_url||0,
more_read_type:more_read_type||0,
rtId:i,
rtKey:a,
appmsg_like_type:window.appmsg_like_type,
is_pay_subscribe:window.isPaySubscribe,
pay_subscribe_uin_count:window.isPaySubscribe?3*d.getCountPerLine():0,
has_red_packet_cover:window.__appmsgCgiData.has_red_packet_cover,
onSuccess:function(t){
if(t)try{
if(window.__second_open__&&t.pay_subscribe_info&&1*t.pay_subscribe_info.is_paid!=isPaid)return _.report110809(11),
(new Image).src="https://badjs.weixinbridge.com/badjs?id=244&level=4&from="+window.encodeURIComponent(window.location.host)+"&msg="+window.encodeURIComponent(window.location.href),
void f.invoke("handleMPPageAction",{
action:"paySuccess",
fullUrl:window.location.href,
itemShowType:window.item_show_type
},function(e){
_.report110809(e.err_msg.indexOf("ok")>-1?19:20),window.localStorage&&window.localStorage.setItem&&window.localStorage.setItem("isPaid-"+window.biz+"-"+window.mid+"-"+window.idx,"1"),
window.location.href=window.location.href+"&r="+Math.random()+"#wechat_redirect";
});
if(t&&t.base_resp&&t.base_resp.wxtoken&&(window.wxtoken=t.base_resp.wxtoken),window.fromWeixinCached&&e("appmsg/iframe.js"),
r(t),t.ret)return;
if(t.red_packet_cover_data&&t.red_packet_cover_data.cover_uri_data&&t.red_packet_cover_data.cover_uri_data.length>0){
var o=e("redpackage/redpacketcover.js");
o.render({
list:t.red_packet_cover_data.cover_uri_data
});
}
var s=document.getElementById("js_more_read_area");
s&&t&&t.more_read_list&&t.more_read_list.length&&e("appmsg/more_read.js")(s,t.more_read_list),
window.isFans=t.is_fans,n({
appmsgstat:t.appmsgstat,
comment_enabled:t.comment_enabled,
comment_count:t.comment_count,
friend_comment_enabled:t.friend_comment_enabled,
only_fans_can_comment:t.only_fans_can_comment,
only_fans_days_can_comment:t.only_fans_days_can_comment,
is_fans_days:t.is_fans_days,
reward:{
reward_total:t.reward_total_count,
is_reward_total_count_cut:t.is_reward_total_count_cut,
reward_head_imgs:t.reward_head_imgs||[],
can_reward:t.can_reward,
user_can_reward:t.user_can_reward,
reward_qrcode_ticket:t.reward_qrcode_ticket,
timestamp:t.timestamp,
reward_author_head:t.reward_author_head,
rewardsn:t.rewardsn,
scene:source,
is_need_reward:is_need_reward,
title:msg_title,
author_id:author_id,
appmsgextRtId:i,
appmsgextRtKey:a,
can_whisper:t.can_whisper
},
reward_entrance_enable_for_preview:t.reward_entrance_enable_for_preview,
reward_wording:t.reward_wording,
reward_author_head:t.reward_author_head,
comment_entrance_enable_for_preview:t.comment_entrance_enable_for_preview,
share_redirect_url:t.share_redirect_url||"",
logo_url:t.logo_url,
nick_name:t.nick_name,
is_fans:t.is_fans,
paySubscribeInfo:t.pay_subscribe_info
});
}catch(d){
v("[Appmsg] error parse async data, biz="+biz+", mid="+mid);
var c=new Image;
return c.src=("http://mp.weixin.qq.com/mp/jsreport?1=1&key=1&content=biz:"+biz+",mid:"+mid+",uin:"+uin+"[key1]"+encodeURIComponent(d.toString())+"&r="+Math.random()).substr(0,1024),
void(console&&console.error(d));
}
},
onError:function(){
var e=new Image;
e.src="http://mp.weixin.qq.com/mp/jsreport?1=1&key=2&content=biz:"+biz+",mid:"+mid+",uin:"+uin+"[key2]ajax_err&r="+Math.random();
}
});
}
e("biz_wap/ui/weui.js"),e("biz_common/utils/string/html.js");
var s=e("appmsg/reward_utils.js"),d=e("appmsg/pay_read_utils.js"),_=e("appmsg/pay_report_utils.js"),c=e("pages/create_txv.js"),m=e("pages/video_ctrl.js"),p=e("biz_common/utils/url/parse.js"),l=e("appmsg/img_copyright_tpl.html.js"),w=e("appmsg/appmsgext.js"),u=e("appmsg/share_tpl.html.js"),g=navigator.userAgent,h=-1!=g.indexOf("MicroMessenger"),y=(-1!=navigator.userAgent.indexOf("WindowsWechat"),
e("biz_common/dom/event.js")),f=(e("biz_wap/utils/ajax.js"),e("biz_wap/jsapi/core.js")),b=e("biz_common/tmpl.js"),v=(e("complain/localstorage.js"),
e("appmsg/log.js")),j=(e("rt/appmsg/getappmsgext.rt.js"),e("a/a_utils.js")),k=e("appmsg/related_article.js"),x=[],z=e("appmsg/set_font_size.js").setFontSize,I=e("biz_wap/utils/device.js"),S=e("biz_wap/utils/mmversion.js"),A=!1;
t();
var E=function(){};
o(),(!window.isPaySubscribe||window.isPaySubscribe&&window.isPaid)&&hasRelatedArticleInfo&&k(function(e,t){
A=!0,"error"==e?E():(E(),t());
});
});define("biz_wap/ui/lazyload_img.js",["biz_wap/utils/mmversion.js","biz_common/dom/event.js","biz_common/dom/attr.js","biz_common/ui/imgonepx.js"],function(t){
"use strict";
function i(){
var t=this.images;
if(!t||t.length<=0)return!1;
var i=window.pageYOffset||document.documentElement.scrollTop,e=window.innerHeight||document.documentElement.clientHeight,o=this.offset||60,n=0;
if("wifi"==window.networkType){
var s={
bottom:1,
top:1
};
this.lazyloadHeightWhenWifi&&(s=this.lazyloadHeightWhenWifi()),o=Math.max(s.bottom*e,o),
n=Math.max(s.top*e,n);
}
for(var r=+new Date,c=[],d=this.sw,f=this,g=-1,u=0,p=t.length;p>u;u++)!function(t,i){
var s=t.el.getBoundingClientRect(),r=t.src;
if(r){
(r.match(/\:\/\/[^\/]+\/mmbiz\//)&&r.indexOf("wx_fmt=gif")>-1||r.match(/\:\/\/[^\/]+\/mmbiz_gif\//))&&g++;
var f=n,u=o;
(r.match(/\:\/\/[^\/]+\/mmbiz\//)&&r.indexOf("wx_fmt=gif")>-1||r.match(/\:\/\/[^\/]+\/mmbiz_gif\//))&&l&&(f=0,
u=60),!t.show&&(s.top<=0&&s.top+s.height+f>=0||s.top>0&&s.top<e+u)&&(i.inImgRead&&(s.top<=0&&s.top+s.height>=0||s.top>0&&s.top<e)&&i.inImgRead(r,networkType),
i.changeSrc&&(r=i.changeSrc(t.el,r,g)),t.el.onerror=function(){
var e=this;
!!i.onerror&&i.onerror(t.el.src,e);
},t.el.onload=function(){
var e=this;
if("data:image/gif;base64,iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVQImWNgYGBgAAAABQABh6FO1AAAAABJRU5ErkJggg=="!=e.src){
var o=e.getAttribute("data-forceheight");
o?(e.removeAttribute("data-forceheight"),h(e,"height",o,"important")):h(e,"height","auto","important"),
e.getAttribute("_width")?h(e,"width",e.getAttribute("_width"),"important"):h(e,"width","auto","important"),
!!i.onload&&i.onload(t.el.src,e);
}
},m(t.el,"src",r),c.push(r),t.show=!0,h(t.el,"visibility","visible","important")),
a.isWp&&1*t.el.width>d&&(t.el.width=d);
}
}(t[u],f);
c.length>0&&this.detect&&this.detect({
time:r,
loadList:c,
scrollTop:i
});
}
function e(){
var t=document.getElementsByTagName("img"),e=[],o=this.container,n=this.attrKey||"data-src",a=o.offsetWidth,s=0,r=this.imgOccupied||!1,l=this.crossOrigin||!1;
o.currentStyle?s=o.currentStyle.width:"undefined"!=typeof getComputedStyle&&(s=getComputedStyle(o).width),
this.sw=1*s.replace("px","");
for(var d=0,f=t.length;f>d;d++){
var g=t.item(d),u=m(g,n),p=m(g,"src");
if(u&&!(p&&p.indexOf("data:image/gif;base64")<0)){
var w=100;
if(g.dataset&&g.dataset.ratio){
var A=1*g.dataset.ratio,b=1*g.dataset.w||a;
"number"==typeof A&&A>0?(b=a>=b?b:a,w=b*A,r||(g.style.width&&g.setAttribute("_width",g.style.width),
h(g,"width",b+"px","important"),h(g,"visibility","visible","important"),g.setAttribute("src",c))):h(g,"visibility","hidden","important");
}else h(g,"visibility","hidden","important");
r||h(g,"height",w+"px","important"),l&&-1==u.indexOf("mmsns.qpic.cn")&&!(u.match(/\:\/\/[^\/]+\/mmbiz\//)&&u.indexOf("wx_fmt=gif")>-1||u.match(/\:\/\/[^\/]+\/mmbiz_gif\//))&&(g.crossOrigin="anonymous"),
e.push({
el:g,
src:u,
height:w,
show:!1
});
}
}
this.images=e,i.call(this);
}
function o(t){
if(this.__called_first_time)i.call(this,t),this.__called_first_time=!1;else if(!this.debounce){
this.debounce=!0;
var e=this;
setTimeout(function(){
i.call(e,t),e.debounce=!1;
},500);
}
}
function n(t){
s.on(window,"scroll",function(i){
o.call(t,i);
}),setTimeout(function(){
e.call(t,{});
},0),s.on(document,"touchmove",function(i){
o.call(t,i);
}),t.__called_first_time=!0,o.call(t,{});
}
var a=t("biz_wap/utils/mmversion.js"),s=t("biz_common/dom/event.js"),r=t("biz_common/dom/attr.js"),m=r.attr,h=r.setProperty,c=t("biz_common/ui/imgonepx.js"),l=!0;
return n;
});