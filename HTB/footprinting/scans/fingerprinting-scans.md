
```shell
➜  ~ htbuser curl -I http://app.inlanefreight.local --resolve app.inlanefreight.local:80:10.129.104.9

HTTP/1.1 200 OK
Date: Fri, 13 Jun 2025 00:37:52 GMT
Server: Apache/2.4.41 (Ubuntu)
Set-Cookie: 72af8f2b24261272e581a49f5c56de40=d492v5abh4goj0ah9c2a9gm3ph; path=/; HttpOnly
Permissions-Policy: interest-cohort=()
Expires: Wed, 17 Aug 2005 00:00:00 GMT
Last-Modified: Fri, 13 Jun 2025 00:38:01 GMT
Cache-Control: no-store, no-cache, must-revalidate, post-check=0, pre-check=0
Pragma: no-cache
Content-Type: text/html; charset=utf-8
```

- Determine the Apache version running on app.inlanefreight.local on the target system. (Format: 0.0.0)
	- 2.4.41

```shell
➜  ~ htbuser curl http://app.inlanefreight.local --resolve app.inlanefreight.local:80:10.129.104.9

<!DOCTYPE html>
<html lang="en-gb" dir="ltr">
<head>
	<meta name="viewport" content="width=device-width, initial-scale=1.0" />
	<meta charset="utf-8" />
	<base href="http://app.inlanefreight.local/" />
	<meta name="generator" content="Joomla! - Open Source Content Management" />
	<title>Home</title>
	<link href="/index.php?format=feed&amp;type=rss" rel="alternate" type="application/rss+xml" title="RSS 2.0" />
	<link href="/index.php?format=feed&amp;type=atom" rel="alternate" type="application/atom+xml" title="Atom 1.0" />
	<link href="/templates/protostar/favicon.ico" rel="shortcut icon" type="image/vnd.microsoft.icon" />
	<link href="http://app.inlanefreight.local/index.php/component/search/?layout=blog&amp;id=9&amp;Itemid=101&amp;format=opensearch" rel="search" title="Search Inlanefreight Blog" type="application/opensearchdescription+xml" />
	<link href="/templates/protostar/css/template.css?9cf4ead339321a76adad02c5286bbfa4" rel="stylesheet" />
	<link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet" />
	<style>

	h1, h2, h3, h4, h5, h6, .site-title {
		font-family: 'Open Sans', sans-serif;
	}
	body.site {
		border-top: 3px solid #0088cc;
		background-color: #f4f6f7;
	}
	a {
		color: #0088cc;
	}
	.nav-list > .active > a,
	.nav-list > .active > a:hover,
	.dropdown-menu li > a:hover,
	.dropdown-menu .active > a,
	.dropdown-menu .active > a:hover,
	.nav-pills > .active > a,
	.nav-pills > .active > a:hover,
	.btn-primary {
		background: #0088cc;
div.mod_search87 input[type="search"]{ width:auto; }
	</style>
	<script src="/media/jui/js/jquery.min.js?9cf4ead339321a76adad02c5286bbfa4"></script>
	<script src="/media/jui/js/jquery-noconflict.js?9cf4ead339321a76adad02c5286bbfa4"></script>
	<script src="/media/jui/js/jquery-migrate.min.js?9cf4ead339321a76adad02c5286bbfa4"></script>
	<script src="/media/system/js/caption.js?9cf4ead339321a76adad02c5286bbfa4"></script>
	<script src="/media/jui/js/bootstrap.min.js?9cf4ead339321a76adad02c5286bbfa4"></script>
	<script src="/templates/protostar/js/template.js?9cf4ead339321a76adad02c5286bbfa4"></script>
	<!--[if lt IE 9]><script src="/media/jui/js/html5.js?9cf4ead339321a76adad02c5286bbfa4"></script><![endif]-->
	<!--[if lt IE 9]><script src="/media/system/js/html5fallback.js?9cf4ead339321a76adad02c5286bbfa4"></script><![endif]-->
	<script>
jQuery(window).on('load',  function() {
				new JCaption('img.caption');
			});
	</script>

</head>
<body class="site com_content view-category layout-blog no-task itemid-101">
	<!-- Body -->
	<div class="body" id="top">
		<div class="container">
			<!-- Header -->
			<header class="header" role="banner">
				<div class="header-inner clearfix">
					<a class="brand pull-left" href="/">
						<span class="site-title" title="Inlanefreight Blog">Inlanefreight Blog</span>									</a>
					<div class="header-search pull-right">
						<div class="search mod_search87">
	<form action="/index.php" method="post" class="form-inline" role="search">
		<label for="mod-search-searchword87" class="element-invisible">Search ...</label> <input name="searchword" id="mod-search-searchword87" maxlength="200"  class="inputbox search-query input-medium" type="search" size="20" placeholder="Search ..." />		<input type="hidden" name="task" value="search" />
		<input type="hidden" name="option" value="com_search" />
		<input type="hidden" name="Itemid" value="101" />
	</form>
</div>

					</div>
				</div>
			</header>
							<nav class="navigation" role="navigation">
					<div class="navbar pull-left">
						<a class="btn btn-navbar collapsed" data-toggle="collapse" data-target=".nav-collapse">
							<span class="element-invisible">Toggle Navigation</span>
							<span class="icon-bar"></span>
							<span class="icon-bar"></span>
							<span class="icon-bar"></span>
						</a>
					</div>
					<div class="nav-collapse">
						<ul class="nav menu nav-pills mod-list">
<li class="item-101 default current active"><a href="/index.php" >Home</a></li><li class="item-108"><a href="/index.php/about" >About</a></li><li class="item-115"><a href="/index.php/author-login" >Author Login</a></li></ul>

					</div>
				</nav>
						
			<div class="row-fluid">
								<main id="content" role="main" class="span9">
					<!-- Begin Content -->
							<div class="moduletable">
						

<div class="custom"  >
	<p><img src="/images/headers/raindrops.jpg" alt="" /></p></div>
		</div>
	
					<div id="system-message-container">
	</div>

					<div class="blog" itemscope itemtype="https://schema.org/Blog">
	
		
	
	
	
				<div class="items-leading clearfix">
							<div class="leading-0"
					itemprop="blogPost" itemscope itemtype="https://schema.org/BlogPosting">
					
	<div class="page-header">
					<h2 itemprop="name">
									<a href="/index.php/3-welcome-to-your-blog" itemprop="url">
						Welcome to your blog				</a>
							</h2>
		
		
		
			</div>

	
<div class="icons">
	
					<div class="btn-group pull-right">
				<button class="btn dropdown-toggle" type="button" id="dropdownMenuButton-3" aria-label="User tools"
				data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
					<span class="icon-cog" aria-hidden="true"></span>
					<span class="caret" aria-hidden="true"></span>
				</button>
								<ul class="dropdown-menu" aria-labelledby="dropdownMenuButton-3">
											<li class="print-icon"> <a href="/index.php/3-welcome-to-your-blog?tmpl=component&amp;print=1&amp;layout=default" title="Print article < Welcome to your blog >" onclick="window.open(this.href,'win2','status=no,toolbar=no,scrollbars=yes,titlebar=no,menubar=no,resizable=yes,width=640,height=480,directories=no,location=no'); return false;" rel="nofollow">			<span class="icon-print" aria-hidden="true"></span>
		Print	</a> </li>
												</ul>
			</div>
		
	</div>


			<dl class="article-info muted">

		
			<dt class="article-info-term">
									Details			</dt>

							<dd class="createdby" itemprop="author" itemscope itemtype="https://schema.org/Person">
					Written by <span itemprop="name">Joomla</span>	</dd>
			
			
			
			
			
		
					
			
						</dl>




<p>This is a sample blog posting.</p><p>If you log in to the site (the Author Login link is on the very bottom of this page) you will be able to edit it and all of the other existing articles. You will also be able to create a new article and make other changes to the site.</p><p>As you add and modify articles you will see how your site changes and also how you can customise it in various ways.</p><p>Go ahead, you can't break it.</p>



				</div>
											<div class="leading-1"
					itemprop="blogPost" itemscope itemtype="https://schema.org/BlogPosting">
					
	<div class="page-header">
					<h2 itemprop="name">
									<a href="/index.php/4-about-your-home-page" itemprop="url">
						About your home page				</a>
							</h2>
		
		
		
			</div>

	
<div class="icons">
	
					<div class="btn-group pull-right">
				<button class="btn dropdown-toggle" type="button" id="dropdownMenuButton-4" aria-label="User tools"
				data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
					<span class="icon-cog" aria-hidden="true"></span>
					<span class="caret" aria-hidden="true"></span>
				</button>
								<ul class="dropdown-menu" aria-labelledby="dropdownMenuButton-4">
											<li class="print-icon"> <a href="/index.php/4-about-your-home-page?tmpl=component&amp;print=1&amp;layout=default" title="Print article < About your home page >" onclick="window.open(this.href,'win2','status=no,toolbar=no,scrollbars=yes,titlebar=no,menubar=no,resizable=yes,width=640,height=480,directories=no,location=no'); return false;" rel="nofollow">			<span class="icon-print" aria-hidden="true"></span>
		Print	</a> </li>
												</ul>
			</div>
		
	</div>


			<dl class="article-info muted">

		
			<dt class="article-info-term">
									Details			</dt>

							<dd class="createdby" itemprop="author" itemscope itemtype="https://schema.org/Person">
					Written by <span itemprop="name">Joomla</span>	</dd>
			
			
			
			
			
		
					
			
						</dl>




<p>Your home page is set to display the four most recent articles from the blog category in a column. Then there are links to the next two oldest articles. You can change those numbers by editing the content options settings in the blog tab in your site administrator. There is a link to your site administrator in the top menu.</p><p>If you want to have your blog post broken into two parts, an introduction and then a full length separate page, use the Read More button to insert a break.</p>


	
<p class="readmore">
			<a class="btn" href="/index.php/4-about-your-home-page" itemprop="url" aria-label="Read more:  About your home page">
			<span class="icon-chevron-right" aria-hidden="true"></span> 
			Read more: 			About your home page		</a>
	</p>



				</div>
											<div class="leading-2"
					itemprop="blogPost" itemscope itemtype="https://schema.org/BlogPosting">
					
	<div class="page-header">
					<h2 itemprop="name">
									<a href="/index.php/5-your-modules" itemprop="url">
						Your Modules					</a>
							</h2>
		
		
		
			</div>

	
<div class="icons">
	
					<div class="btn-group pull-right">
				<button class="btn dropdown-toggle" type="button" id="dropdownMenuButton-5" aria-label="User tools"
				data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
					<span class="icon-cog" aria-hidden="true"></span>
					<span class="caret" aria-hidden="true"></span>
				</button>
								<ul class="dropdown-menu" aria-labelledby="dropdownMenuButton-5">
											<li class="print-icon"> <a href="/index.php/5-your-modules?tmpl=component&amp;print=1&amp;layout=default" title="Print article < Your Modules >" onclick="window.open(this.href,'win2','status=no,toolbar=no,scrollbars=yes,titlebar=no,menubar=no,resizable=yes,width=640,height=480,directories=no,location=no'); return false;" rel="nofollow">			<span class="icon-print" aria-hidden="true"></span>
		Print	</a> </li>
												</ul>
			</div>
		
	</div>


			<dl class="article-info muted">

		
			<dt class="article-info-term">
									Details			</dt>

							<dd class="createdby" itemprop="author" itemscope itemtype="https://schema.org/Person">
					Written by <span itemprop="name">Joomla</span>	</dd>
			
			
			
			
			
		
					
			
						</dl>




<p>Your site has some commonly used modules already preconfigured. These include:</p><ul><li>Image Module which holds the image beneath the menu. This is a Custom module that you can edit to change the image.</li><li>Most Read Posts which lists articles based on the number of times they have been read.</li><li>Older Articles which lists out articles by month.</li><li>Syndicate which allows your readers to read your posts in a news reader.</li><li>Popular Tags, which will appear if you use tagging on your articles. Just enter a tag in the Tags field when editing.</li></ul><p>Each of these modules has many options which you can experiment with in the Module Manager in your site Administrator. Moving your mouse over a module and clicking on the edit icon will take you to an edit screen for that module. Always be sure to save and close any module you edit.</p><p>Joomla! also includes many other modules you can incorporate in your site. As you develop your site you may want to add more module that you can find at the <a href="https://extensions.joomla.org/">Joomla Extensions Directory.</a></p>



				</div>
											<div class="leading-3"
					itemprop="blogPost" itemscope itemtype="https://schema.org/BlogPosting">
					
	<div class="page-header">
					<h2 itemprop="name">
									<a href="/index.php/6-your-template" itemprop="url">
						Your Template					</a>
							</h2>
		
		
		
			</div>

	
<div class="icons">
	
					<div class="btn-group pull-right">
				<button class="btn dropdown-toggle" type="button" id="dropdownMenuButton-6" aria-label="User tools"
				data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
					<span class="icon-cog" aria-hidden="true"></span>
					<span class="caret" aria-hidden="true"></span>
				</button>
								<ul class="dropdown-menu" aria-labelledby="dropdownMenuButton-6">
											<li class="print-icon"> <a href="/index.php/6-your-template?tmpl=component&amp;print=1&amp;layout=default" title="Print article < Your Template >" onclick="window.open(this.href,'win2','status=no,toolbar=no,scrollbars=yes,titlebar=no,menubar=no,resizable=yes,width=640,height=480,directories=no,location=no'); return false;" rel="nofollow">			<span class="icon-print" aria-hidden="true"></span>
		Print	</a> </li>
												</ul>
			</div>
		
	</div>


			<dl class="article-info muted">

		
			<dt class="article-info-term">
									Details			</dt>

							<dd class="createdby" itemprop="author" itemscope itemtype="https://schema.org/Person">
					Written by <span itemprop="name">Joomla</span>	</dd>
			
			
			
			
			
		
					
			
						</dl>




<p>Templates control the look and feel of your website.</p><p>This blog is installed with the Protostar template.</p><p>You can edit the options by clicking on the Working on Your Site, Template Settings link in the top menu (visible when you login).</p><p>For example you can change the site background color, highlights color, site title, site description and title font used.</p><p>More options are available in the site administrator. You may also install a new template using the extension manager.</p>



				</div>
									</div><!-- end items-leading -->
	
	
	
	
		</div>

					<div class="clearfix"></div>
					<div aria-label="Breadcrumbs" role="navigation">
	<ul itemscope itemtype="https://schema.org/BreadcrumbList" class="breadcrumb">
					<li>
				You are here: &#160;
			</li>
		
						<li itemprop="itemListElement" itemscope itemtype="https://schema.org/ListItem" class="active">
					<span itemprop="name">
						Home					</span>
					<meta itemprop="position" content="1">
				</li>
				</ul>
</div>

					<!-- End Content -->
				</main>
									<div id="aside" class="span3">
						<!-- Begin Right Sidebar -->
						<div class="well "><h3 class="page-header">Older Posts</h3><ul class="category-module mod-list">
						<li>
									<a class="mod-articles-category-title " href="/index.php/3-welcome-to-your-blog">Welcome to your blog</a>
				
				
				
				
				
				
				
							</li>
					<li>
									<a class="mod-articles-category-title " href="/index.php/4-about-your-home-page">About your home page</a>
				
				
				
				
				
				
				
							</li>
					<li>
									<a class="mod-articles-category-title " href="/index.php/5-your-modules">Your Modules</a>
				
				
				
				
				
				
				
							</li>
					<li>
									<a class="mod-articles-category-title " href="/index.php/6-your-template">Your Template</a>
				
				
				
				
				
				
				
							</li>
			</ul>
</div><div class="well "><h3 class="page-header">Most Read Posts</h3><ul class="mostread mod-list">
	<li itemscope itemtype="https://schema.org/Article">
		<a href="/index.php/3-welcome-to-your-blog" itemprop="url">
			<span itemprop="name">
				Welcome to your blog			</span>
		</a>
	</li>
	<li itemscope itemtype="https://schema.org/Article">
		<a href="/index.php/4-about-your-home-page" itemprop="url">
			<span itemprop="name">
				About your home page			</span>
		</a>
	</li>
	<li itemscope itemtype="https://schema.org/Article">
		<a href="/index.php/5-your-modules" itemprop="url">
			<span itemprop="name">
				Your Modules			</span>
		</a>
	</li>
	<li itemscope itemtype="https://schema.org/Article">
		<a href="/index.php/6-your-template" itemprop="url">
			<span itemprop="name">
				Your Template			</span>
		</a>
	</li>
</ul>
</div><div class="well "><a href="/index.php?format=feed&amp;type=rss" class="syndicate-module">
	<img src="/media/system/images/livemarks.png" alt="feed-image" />			<span>
					My Blog				</span>
	</a>
</div>
						<!-- End Right Sidebar -->
					</div>
							</div>
		</div>
	</div>
	<!-- Footer -->
	<footer class="footer" role="contentinfo">
		<div class="container">
			<hr />
			<ul class="nav menu mod-list">
<li class="item-102"><a href="/index.php/login" >Author Login</a></li></ul>

			<p class="pull-right">
				<a href="#top" id="back-top">
					Back to Top				</a>
			</p>
			<p>
				&copy; 2025 Inlanefreight Blog			</p>
		</div>
	</footer>
	
</body>
</html>
```

```shell
➜  ~ echo '10.129.104.9 app.inlanefreight.local dev.inlanefreight.local' | sudo tee -a /etc/hosts

10.129.104.9 app.inlanefreight.local dev.inlanefreight.local

➜  ~ htbuser whatweb http://app.inlanefreight.local

http://app.inlanefreight.local [200 OK] Apache[2.4.41], Bootstrap, Cookies[72af8f2b24261272e581a49f5c56de40], Country[RESERVED][ZZ], HTML5, HTTPServer[Ubuntu Linux][Apache/2.4.41 (Ubuntu)], HttpOnly[72af8f2b24261272e581a49f5c56de40], IP[10.129.104.9], JQuery, MetaGenerator[Joomla! - Open Source Content Management], OpenSearch[http://app.inlanefreight.local/index.php/component/search/?layout=blog&amp;id=9&amp;Itemid=101&amp;format=opensearch], Script, Title[Home], UncommonHeaders[permissions-policy]
```

- Which CMS is used on app.inlanefreight.local on the target system? Respond with the name only, e.g., WordPress. 
	- Joomla

```shell
➜  ~ htbuser whatweb http://dev.inlanefreight.local

http://dev.inlanefreight.local [200 OK] Apache[2.4.41], Bootstrap, Cookies[02a93f6429c54209e06c64b77be2180d], Country[RESERVED][ZZ], HTML5, HTTPServer[Ubuntu Linux][Apache/2.4.41 (Ubuntu)], HttpOnly[02a93f6429c54209e06c64b77be2180d], IP[10.129.104.9], JQuery, MetaGenerator[Joomla! - Open Source Content Management], OpenSearch[http://dev.inlanefreight.local/index.php/component/search/?layout=blog&amp;id=9&amp;Itemid=101&amp;format=opensearch], Script, Title[Home]
```

-  On which operating system is the dev.inlanefreight.local webserver running in the target system? Respond with the name only, e.g., Debian. 
	- Ubuntu