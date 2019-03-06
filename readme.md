執行Sling Server: 
E:/java/
java -jar org.apache.sling.starter-11.jar
---------------------------------------------
eclipse安裝Sling IDE
https://sling.apache.org/documentation/development/ide-tooling.html

Unable to create project from archetype [org.apache.sling:sling-bundle-archetype:1.0.6 -> http://repo1.maven.org/maven2/]
---------------------------------------------
eclipse匯出匯入Sling server
eclipse設定好Server後, 專案右鍵Sling->Export/Import to server
---------------------------------------------
改Router路徑: 
META-INF/vault/filter.xml

<workspaceFilter vesion="1.0">
    <filter root="/content/podcasts"/>
    <filter root="/apps/components"/>
</workspaceFilter>
---------------------------------------------
.content.xml
->要在目錄中加入這個才會產生json?
->導向app目錄=><jcr:root sling:resourceType="components/podcasts"></jcr:root>

http://localhost:8080/static.tidy.4.json
可以看static目錄下有甚麼檔案
http://localhost:8080/static.json
只看static目錄狀態為何
---------------------------------------------
/app    
該目錄為html層

讀取資料範例:

${ properties.jcr:title }

<div data-sly-list="${ resource.listChildren }">
	<p>${ item.name }</p>
	<p>${ item.jcr:title }</p>
	<p>${ item.jcr:description }</p>
</div>

---------------------------------------------
/content
該目錄為data層

<jcr:root 內設定
sling:resourceType="components/podcasts" 
-> 輸入http://localhost:8080/content/podcasts.html
-> 將會引導至/app/components/podcasts/html.html這個檔案

---------------------------------------------
HTL指令詳解:
https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/block-statements.html
https://docs.adobe.com/content/help/en/experience-manager-htl/using/htl/global-objects.html
https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md
http://blogs.adobe.com/experiencedelivers/experience-management/htl-intro-part-2/

標題
jcr:title=""

描述(SEO用)
jcr:description=""

Include
<head data-sly-include="${'/apps/components/header.html'}"></head>

印出子節點相關資訊
<div data-sly-list="${ resource.listChildren }">
	<p>${ item.name }</p>
	<p>${ item.jcr:title }</p>
	<p>${ item.jcr:description }</p>
</div>

動態製造超連結網址
<a href="${ item.name @ prependPath='podcasts/', addSelectors=['html'] }" class="list-group-item"></a>
->'podcasts/' + item.name + '.html'

下面最後要接斜線, 沒加的話會變成修改/content/podcasts這個目錄, 加了後會導向該目錄下再新增子目錄
<form method="post" action="/content/podcasts/">
<input type="hidden" name="sling:resourceType" value="components/podcasts/">

送出後自動轉網址
<input type="hidden" name=":redirect" value="/content/podcasts.html" />

加上這個才會自動將post出來的值用UTF-8傳送
<input type="hidden" name="_charset_" value="UTF-8"/>

---------------------------------------------
設定目錄的jcr:primaryType
可從這網址進去修改 http://localhost:8080/bin/browser.html/
nt:folder can be used as a "vanilla" folder node in the JCR
sling:folder allows the folders children to be interpreted using their sling:resourceType — e.g. if you had a node "bar" at /etc/designs/foo/bar, setting the resource type of "foo" to a sling:Folder allows you to resolve bar using its resource type via a script (just like with components), whereas if "foo" were an nt:folder this wouldn't be possible (it would just be treated statically).
sling:OrderedFolder can be used when ordering is important, e.g. in the /etc/map directory, if you want your entries to be used in order rather than randomly, the ordered folder provides this option. (For most cases, it's not really needed.)
---------------------------------------------
Sling post servlet
文件
https://sling.apache.org/documentation/bundles/manipulating-content-the-slingpostservlet-servlets-post.html
---------------------------------------------
.Java
currentPage.getTitle()
getResource()
getPageManager()
---------------------------------------------
Youtube教學:
https://www.youtube.com/watch?v=sklauzjfO8w&list=PLlf_Fk4pk-ggCdBr94XEcBJ6EAFU019VB&index=1
---------------------------------------------
1.登入AEM
http://localhost:4502
2.Create pages using templates
3.Create the content for my website
....待補
---------------------------------------------
AEM教學
https://www.youtube.com/watch?v=OgYMw3sxCCU&feature=youtu.be
https://helpx.adobe.com/tw/support/experience-manager/6-4.html
https://helpx.adobe.com/tw/support/experience-manager/6-3.html
---------------------------------------------
AEM提供以下內容：
Web應用程序服務器：AEM可以以獨立模式（包括集成的Jetty Web服務器）部署，也可以作為第三方應用程序服務器（WebLogic，WebSphere等）中的Web應用程序部署。
Web應用程序框架：AEM包含Sling Web應用程序框架，該框架簡化了RESTful，面向內容的Web應用程序的編寫。
內容存儲庫：AEM包括Java內容存儲庫（JCR），這是一種專門為非結構化和半結構化數據設計的分層數據庫。存儲庫不僅存儲面向用戶的內容，還存儲應用程序使用的所有代碼，模板和內部數據。

安裝方法
https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/deploy.html
https://helpx.adobe.com/experience-manager/6-4/sites/deploying/using/application-server-install.html


project->packages->可安裝元件
CRXDE Lite線上編輯程式碼

apps
->右鍵create templete -> 可開始寫HTML
->右鍵create component -> 可開始寫JSP

AEM視窗下方選Design可以選擇很多東西拖拉到介面中
http://docs.adodb.com/docs/en/aem/6-3/develop/ref/widgets-api/index.html?classCQ.Ext.layout.ContainerLayout
---------------------------------------------








demo:
http://localhost:8080/podcasts.html

http://localhost:8080/podcasts.add.html

http://localhost:8080/podcasts.testHTL.html


http://localhost:8080/Animal/animal



