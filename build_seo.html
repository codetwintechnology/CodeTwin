from bs4 import BeautifulSoup
from pathlib import Path
import json, re, shutil, zipfile, os

root=Path('/mnt/data/seo_work')
site_url='https://YOUR-DOMAIN-HERE.com'
brand='CodeTwin Technology'
phone='919987397999'
logo='logo.jpeg'

page_meta={
'index.html':('Website Development Company in Rajkot | CodeTwin Technology','CodeTwin Technology builds websites, mobile apps, custom software, UI/UX and digital marketing solutions for businesses in Rajkot, Gujarat.'),
'about.html':('About CodeTwin Technology | Digital Solutions in Rajkot','Learn about CodeTwin Technology, a Rajkot, Gujarat digital development studio delivering websites, mobile apps, software, UI/UX and online marketing solutions.'),
'services.html':('Web, App & Software Development Services in Rajkot','Explore CodeTwin Technology services in Rajkot, Gujarat: website development, mobile apps, custom software, UI/UX, Google Ads, Meta Ads and digital solutions.'),
'projects.html':('Web, Mobile & Software Projects | CodeTwin Technology','Explore CodeTwin Technology project examples including business websites, mobile products, dashboards and lead-generation systems built for digital growth.'),
'contact.html':('Contact CodeTwin Technology in Rajkot | Start a Project','Contact CodeTwin Technology in Rajkot, Gujarat for website development, mobile apps, custom software, UI/UX, Google Ads and Meta Ads projects.'),
}

# Shared schema helpers
org={
'@type':'Organization','@id':site_url+'/#organization','name':brand,'url':site_url,'logo':site_url+'/'+logo,
'description':'Digital development and marketing studio providing websites, mobile apps, custom software, UI/UX and advertising solutions.',
'areaServed':{'@type':'City','name':'Rajkot'},'sameAs':[]
}
local={
'@type':'LocalBusiness','@id':site_url+'/#localbusiness','name':brand,'url':site_url,'image':site_url+'/'+logo,
'priceRange':'$$','telephone':'+91 9987397999','address':{'@type':'PostalAddress','addressLocality':'Rajkot','addressRegion':'Gujarat','addressCountry':'IN'},
'areaServed':{'@type':'City','name':'Rajkot'}
}

def schema_script(data):
    return '<script type="application/ld+json">'+json.dumps(data,ensure_ascii=False,separators=(',',':'))+'</script>'

def add_common_head(soup, filename):
    title,desc=page_meta[filename]
    soup.title.string=title
    md=soup.find('meta',attrs={'name':'description'})
    if md: md['content']=desc
    else:
        md=soup.new_tag('meta',attrs={'name':'description','content':desc}); soup.head.append(md)
    # keywords kept modest; not a ranking requirement, but useful as an internal content signal only
    kw='website development Rajkot, mobile app development Rajkot, custom software Rajkot, UI UX design, Google Ads, Meta Ads, digital marketing'
    old=soup.find('meta',attrs={'name':'keywords'})
    if old: old['content']=kw
    else: soup.head.append(soup.new_tag('meta',attrs={'name':'keywords','content':kw}))
    # canonical placeholder is centralized for easy replacement before launch
    can=soup.find('link',attrs={'rel':'canonical'})
    href=site_url+'/'+filename
    if can: can['href']=href
    else: soup.head.append(soup.new_tag('link',attrs={'rel':'canonical','href':href}))
    # OpenGraph
    for prop,content in [('og:title',title),('og:description',desc),('og:type','website'),('og:url',href),('og:site_name',brand)]:
        t=soup.find('meta',attrs={'property':prop})
        if t:t['content']=content
        else:soup.head.append(soup.new_tag('meta',attrs={'property':prop,'content':content}))
    # twitter
    for name,content in [('twitter:card','summary_large_image'),('twitter:title',title),('twitter:description',desc)]:
        t=soup.find('meta',attrs={'name':name})
        if t:t['content']=content
        else:soup.head.append(soup.new_tag('meta',attrs={'name':name,'content':content}))
    # remove old JSON-LD to avoid conflicting duplicates
    for x in soup.find_all('script',attrs={'type':'application/ld+json'}): x.decompose()
    graph=[org,local,{'@type':'WebSite','@id':site_url+'/#website','name':brand,'url':site_url}]
    soup.head.append(soup.new_tag('script',type='application/ld+json'))
    soup.head.find_all('script',attrs={'type':'application/ld+json'})[-1].string=json.dumps({'@context':'https://schema.org','@graph':graph},separators=(',',':'))

def add_blog_nav(soup):
    for links in soup.select('.links'):
        if not links.find('a',href='blog.html'):
            a=soup.new_tag('a',href='blog.html'); a.string='Blog'; links.append(a)
    for fl in soup.select('.footLinks'):
        if not fl.find('a',href='blog.html'):
            a=soup.new_tag('a',href='blog.html'); a.string='Blog'; fl.append(a)

def ensure_alt(soup):
    for img in soup.find_all('img'):
        if not img.get('alt'):
            src=img.get('src','')
            img['alt']=re.sub(r'[-_]+',' ',Path(src.split('?')[0]).stem).title() or brand

def replace_services_links(soup):
    mapping={
      'Website Development':'website-development.html','Mobile App Development':'mobile-app-development.html','Custom Software':'custom-software-development.html','UI / UX & Design':'ui-ux-design.html','Google Ads':'google-ads.html','Meta Ads':'meta-ads.html','Digital Presence':'digital-marketing.html','Other Development Services':'custom-software-development.html'
    }
    for h in soup.find_all(['h3','h2']):
        text=' '.join(h.stripped_strings)
        for label,url in mapping.items():
            if text==label or text.startswith(label):
                parent=h.parent
                # Add a learn more link in card/section without changing layout structure.
                if not parent.find('a',href=url):
                    a=soup.new_tag('a',href=url,attrs={'class':'serviceLearn'}); a.string='Explore service ↗'; parent.append(a)
                break

# Update base pages
for filename in page_meta:
    path=root/filename
    soup=BeautifulSoup(path.read_text(encoding='utf8'),'html.parser')
    add_common_head(soup,filename); add_blog_nav(soup); ensure_alt(soup)
    if filename=='services.html': replace_services_links(soup)
    # Add small SEO-safe style additions without altering theme
    style=soup.new_tag('style')
    style.string='.serviceLearn{display:inline-flex;margin-top:18px;color:#fff;font:500 11px DM Mono,monospace;letter-spacing:.08em;text-transform:uppercase;border-bottom:1px solid rgba(227,27,35,.45);padding-bottom:5px}.serviceLearn:hover{color:#e31b23}'
    soup.head.append(style)
    path.write_text(str(soup),encoding='utf8')

# Rebuild services page main service cards with links by simple post-processing if appended links are inside h3 parent.

# Service detail content
services={
'website-development.html':{
 'title':'Website Development in Rajkot | CodeTwin Technology','desc':'Professional website development in Rajkot, Gujarat for business, corporate, landing page and e-commerce websites with responsive UX and practical integrations.',
 'name':'Website Development','keyword':'Website Development in Rajkot','icon':'https://cdn.simpleicons.org/html5/E34F26','tag':'01 / WEB',
 'paras':[
 ('Websites built around your business goals','A business website should do more than display information. It should explain what you offer, build trust, guide visitors to the right action and make it easy to contact you. CodeTwin Technology provides website development in Rajkot, Gujarat for businesses that need a modern online presence without losing clarity or speed. We plan the structure around your audience, services, enquiry journey and future growth.'),
 ('Responsive design for every screen','Customers may discover a business from a phone, tablet or desktop. Our responsive approach keeps navigation, content, forms, images and calls to action usable across screen sizes. The goal is a consistent experience rather than a desktop page squeezed onto a mobile screen. We can build business websites, corporate websites, landing pages, portfolio sites and e-commerce experiences with a clean, modern interface.'),
 ('Development, integrations and business workflows','A website often needs to connect with more than a contact form. Depending on the requirement, CodeTwin can integrate APIs, enquiry forms, WhatsApp, analytics, payment or booking flows, admin panels and third-party services. We focus on practical workflows so that a website can support day-to-day business operations instead of becoming another disconnected tool.'),
 ('SEO-friendly foundations','Search visibility starts with a useful page structure. We use descriptive page titles, meta descriptions, logical headings, internal links, image alt text, structured data where appropriate and crawlable site files. These technical foundations help search engines understand the site, while the actual content is written for people first. Local businesses can also build location-relevant pages around Rajkot and the services they genuinely provide.'),
 ('A clear process from idea to launch','The process normally starts with requirements and page planning, followed by UI direction, development, responsive testing, content placement and launch preparation. Existing websites can also be redesigned when the current structure is difficult to use, slow to update or no longer represents the business. After launch, the site can be extended with new pages, integrations, campaigns and content.'),
 ('Built for the next stage of your business','Whether you need a five-page company website or a larger platform with forms, dashboards and integrations, the technology should match the actual requirement. CodeTwin Technology combines development, UI/UX and digital marketing services so the website can connect naturally with future campaigns. If your business is in Rajkot, Gujarat and you need a website that is clear, responsive and ready for growth, the next step is to share your goals and requirements.')
 ]},
'mobile-app-development.html':{
 'title':'Mobile App Development in Rajkot | CodeTwin Technology','desc':'Mobile app development in Rajkot, Gujarat for Android and iOS apps, API integrations, user systems, notifications and business workflows.',
 'name':'Mobile App Development','keyword':'Mobile App Development in Rajkot','icon':'https://cdn.simpleicons.org/android/3DDC84','tag':'02 / APP',
 'paras':[
 ('Mobile apps designed around real use cases','A mobile app is most useful when it solves a specific customer or business problem. CodeTwin Technology develops mobile application experiences for businesses that want a direct digital product for customers, staff or internal workflows. We start with the user journey, required features and backend needs before choosing the implementation approach.'),
 ('Android and iOS experiences','The app experience should feel natural on the platforms your audience uses. Projects can include Android and iOS applications, account flows, forms, notifications, API communication and data-driven screens. The interface is planned around touch interaction, readable layouts and simple navigation so users can complete important actions without unnecessary steps.'),
 ('API, database and business integration','Most useful business apps need a backend. CodeTwin can connect mobile interfaces with APIs, databases, authentication systems and existing business services. This can support customer profiles, product information, bookings, enquiries, orders, notifications or internal dashboards. The exact architecture is selected around the project rather than forcing every business into the same technology stack.'),
 ('UI/UX before development','A good app experience starts before coding. We can map screens and flows in Figma, define reusable interface components and review the journey from onboarding to the core action. This reduces confusion during development and gives the business a clearer view of the product before the full implementation is built.'),
 ('Testing and launch preparation','Mobile projects need testing across screen sizes, navigation states, network conditions and real user workflows. We can review forms, API states, loading behavior, validation and notifications before launch. Launch preparation can also include store-ready assets and the technical configuration required for the selected distribution path.'),
 ('A mobile product that can evolve','The first version of an app should leave room for future features. CodeTwin can plan the project in phases so that a useful initial release can later expand with new modules, integrations, dashboards or marketing campaigns. If you are looking for mobile app development in Rajkot, Gujarat, share the problem you want the app to solve and we can shape the product around it.')
 ]},
'custom-software-development.html':{
 'title':'Custom Software Development in Rajkot | CodeTwin Technology','desc':'Custom software development in Rajkot, Gujarat for dashboards, admin panels, business systems, databases, APIs and workflow automation.',
 'name':'Custom Software Development','keyword':'Custom Software Development in Rajkot','icon':'https://cdn.simpleicons.org/node.js/5FA04E','tag':'03 / SOFTWARE',
 'paras':[
 ('Software built for the way your business works','Off-the-shelf tools can be useful, but some businesses need workflows that do not fit a standard product. CodeTwin Technology develops custom software in Rajkot, Gujarat for businesses that want their processes, data and roles organized in one digital system. We first understand how work happens today and then identify the parts that should be simplified, connected or automated.'),
 ('Dashboards and admin panels','A dashboard can turn scattered information into a practical control center. Depending on the requirement, a custom system can include user management, records, status tracking, reports, permissions, search, filters and operational summaries. Admin panels can also give staff a clearer way to manage the website, app or internal workflow without editing raw data.'),
 ('APIs, databases and integrations','Business software often needs to communicate with other systems. CodeTwin can build or connect APIs, databases and third-party services so information can move between the tools your business already uses. Integrations may support forms, payments, notifications, customer records, reporting or other operational requirements.'),
 ('Automation that reduces repetitive work','If a process repeatedly involves copying data, sending updates, checking records or moving information between tools, software can often reduce that manual effort. Automation should be designed carefully, with clear rules and human control where needed. The goal is not automation for its own sake; it is to make the business process more reliable and easier to manage.'),
 ('Security, roles and maintainability','Business systems often contain information that should not be visible to every user. Custom software can include role-based access, validation and structured data handling. The codebase should also be organized so future developers can understand and extend it. CodeTwin can plan the system with future modules in mind rather than treating the first release as the final version.'),
 ('From workflow map to working system','The project normally moves through requirements, workflow mapping, UI/UX, database and API planning, development, testing and deployment. If your business in Rajkot has a spreadsheet-heavy, manual or disconnected process, a custom software project may provide a clearer long-term workflow. Tell us what currently takes too much time and we can discuss a practical digital approach.')
 ]},
'ui-ux-design.html':{
 'title':'UI UX Design Services in Rajkot | CodeTwin Technology','desc':'UI/UX design in Rajkot, Gujarat for websites and mobile apps using user flows, wireframes, Figma interfaces and practical design systems.',
 'name':'UI / UX Design','keyword':'UI UX Design in Rajkot','icon':'https://cdn.simpleicons.org/figma/F24E1E','tag':'04 / UI UX',
 'paras':[
 ('Design that supports the product','UI/UX is not only about making a screen look attractive. It is about making the next action understandable. CodeTwin Technology designs website and mobile experiences in Rajkot, Gujarat around content, user journeys and business goals. We combine visual hierarchy with practical navigation so users can find information and complete actions more easily.'),
 ('User flows and information structure','Before polishing colors and components, the structure matters. We can map the journey from the first screen to the desired action, identify important content and remove unnecessary steps. For websites this can mean clearer navigation and enquiry paths; for apps it can mean simpler onboarding, account flows and task completion.'),
 ('Figma-based interface design','Figma can be used to create wireframes, high-fidelity screens, reusable components and prototypes before development. This provides a shared reference for the business and development team. It also makes it easier to review a page or screen while changes are still inexpensive.'),
 ('Responsive and accessible thinking','A design should consider different screen sizes, readable text, sufficient contrast, touch targets and clear states for forms or interactive components. These details matter because the same product may be used in different contexts. CodeTwin keeps the design practical so the final implementation can match the intended experience.'),
 ('Design systems and consistency','As a website or app grows, repeated components should remain consistent. A small design system can define buttons, cards, spacing, typography, colors and states. This helps new pages feel like part of the same product and can reduce design and development effort when the product expands.'),
 ('From Figma to development','Because CodeTwin also provides development services, the design can be planned with implementation in mind. That means considering real content, responsive behavior and component reuse instead of creating screens that are difficult to build. If you need UI/UX design in Rajkot, Gujarat for a website, app or custom software product, we can take the project from flow to polished interface.')
 ]},
'google-ads.html':{
 'title':'Google Ads Services in Rajkot | CodeTwin Technology','desc':'Google Ads services in Rajkot, Gujarat for search campaigns, lead generation, landing pages, conversion tracking and performance-focused advertising.',
 'name':'Google Ads','keyword':'Google Ads Services in Rajkot','icon':'https://cdn.simpleicons.org/googleads/4285F4','tag':'05 / GOOGLE',
 'paras':[
 ('Google Ads connected to the right landing experience','Paid search works best when the ad, keyword intent and landing page tell the same story. CodeTwin Technology helps businesses in Rajkot, Gujarat structure Google Ads campaigns around clear goals such as enquiries, calls or qualified leads. We also consider the page a customer reaches after clicking because the ad alone cannot create a good conversion experience.'),
 ('Campaign structure and search intent','Different searches can represent different levels of intent. Campaigns can be organized around services, locations and meaningful search themes so that the message is relevant to the person searching. Ad copy should be clear about the offer and the landing page should make the next step obvious.'),
 ('Lead generation and conversion paths','A campaign may send users to a website form, landing page, call action or another agreed conversion path. CodeTwin can coordinate the landing page, form and enquiry workflow so leads do not get lost between advertising and the business team. The exact setup depends on the service, audience and operational process.'),
 ('Measurement and improvement','Advertising needs measurement to understand what is happening after launch. Useful metrics can include clicks, enquiries, cost per lead and conversion activity. Performance should be reviewed against the business objective rather than chasing a single metric in isolation. Changes can then be made to targeting, messaging, landing pages or campaign structure as the data supports.'),
 ('Website and ads working together','A strong advertising setup often depends on the quality of the website behind it. CodeTwin can combine Google Ads with website development, UI/UX and analytics preparation so the customer journey is connected. This is particularly useful for local businesses that want a clear path from search to enquiry.'),
 ('A practical approach for Rajkot businesses','If your business serves Rajkot or nearby areas, location can be part of the campaign structure where it matches the actual service area. CodeTwin can help plan the advertising journey, landing experience and enquiry flow together. Share your service, target customer and goal and we can discuss an appropriate Google Ads setup.')
 ]},
'meta-ads.html':{
 'title':'Meta Ads Services in Rajkot | CodeTwin Technology','desc':'Meta Ads services in Rajkot, Gujarat for Facebook and Instagram campaigns, lead generation, creative structure, targeting and conversion journeys.',
 'name':'Meta Ads','keyword':'Meta Ads Services in Rajkot','icon':'https://cdn.simpleicons.org/meta/0081FB','tag':'06 / META',
 'paras':[
 ('Social advertising built around a business goal','Facebook and Instagram can support awareness, enquiries and lead-generation campaigns when the message and audience are planned together. CodeTwin Technology provides Meta Ads services in Rajkot, Gujarat with a focus on connecting the campaign to a clear customer journey rather than treating the ad as a standalone creative.'),
 ('Creative, audience and offer alignment','A campaign needs a clear reason for someone to stop, understand the offer and take the next step. We can structure ad concepts around the service, audience and desired action. The creative direction should match the brand and the landing experience should continue the same message after the click.'),
 ('Lead generation journeys','For businesses focused on enquiries, Meta campaigns can be connected to lead forms, landing pages or website enquiry flows. CodeTwin can help organize the journey so the business knows what happens after a person submits an enquiry. This can include a website form, WhatsApp contact path or another agreed workflow.'),
 ('Testing and campaign learning','Digital advertising changes as people respond to different messages and audiences. Campaign management can involve testing creative variations, audience approaches and landing-page messaging while watching the metrics that matter to the business. The goal is to learn from real campaign data and make measured improvements.'),
 ('Meta Ads with your website','When advertising and website content are coordinated, the customer sees a more consistent brand and offer. CodeTwin can connect Meta Ads with website development, UI/UX and analytics preparation so campaign traffic lands on pages designed for the intended action.'),
 ('Local digital growth in Rajkot','If your business serves customers in Rajkot, Gujarat, the campaign can be planned around the areas and audiences you actually serve. CodeTwin can help shape the creative, landing page and enquiry flow around your business. Start by sharing what you sell, who you want to reach and what a successful enquiry looks like.')
 ]},
'digital-marketing.html':{
 'title':'Digital Marketing Company in Rajkot | CodeTwin Technology','desc':'Digital marketing services in Rajkot, Gujarat combining Google Ads, Meta Ads, websites, landing pages, creative direction and conversion-focused digital journeys.',
 'name':'Digital Marketing','keyword':'Digital Marketing Company in Rajkot','icon':'https://cdn.simpleicons.org/instagram/E4405F','tag':'07 / DIGITAL',
 'paras':[
 ('A connected digital presence','Digital marketing is more than posting advertisements. A customer may discover a business through search, social media, a landing page or a recommendation and then visit the website before making an enquiry. CodeTwin Technology brings development and digital marketing together so these touchpoints can work as one system for businesses in Rajkot, Gujarat.'),
 ('Google Ads and Meta Ads','Paid campaigns can serve different parts of the customer journey. Google Ads can reach people actively searching for a service, while Meta Ads can support discovery, awareness and lead-generation campaigns. The appropriate channel depends on the business, audience and goal. We can plan the campaign around the actual service instead of forcing the same approach everywhere.'),
 ('Landing pages and conversion paths','Traffic only becomes useful when the next step is clear. CodeTwin can create or improve landing pages with focused messaging, responsive layouts, enquiry forms and clear calls to action. The page should answer the important questions a visitor has and make contacting the business simple.'),
 ('Creative and brand consistency','Digital campaigns perform within a visual environment where people see many competing messages. Consistent design, clear offers and recognizable brand elements can help a business communicate more professionally. CodeTwin can coordinate campaign visuals with the website and UI/UX direction so the experience feels connected.'),
 ('Measurement and iteration','Digital marketing should be reviewed using meaningful business signals. Depending on the campaign, this may include enquiries, calls, leads, conversion activity and campaign costs. The important part is having a clear measurement path and using the information to improve the next campaign or landing experience.'),
 ('A practical partner for local businesses','For businesses in Rajkot and the surrounding Gujarat market, CodeTwin can combine website development, mobile products, custom software, UI/UX and digital advertising. That means you can start with one requirement and add connected services as the business grows. If you want a digital marketing company in Rajkot that also understands the technology behind the customer journey, tell us what you want to achieve.')
 ]},
}

# Detail page CSS and content
base=BeautifulSoup((root/'services.html').read_text(encoding='utf8'),'html.parser')
# get full head style string from services page, but we will reuse the whole services document then replace main.
for fn,data in services.items():
    soup=BeautifulSoup((root/'services.html').read_text(encoding='utf8'),'html.parser')
    soup.title.string=data['title']
    md=soup.find('meta',attrs={'name':'description'}); md['content']=data['desc']
    can=soup.find('link',attrs={'rel':'canonical'}); can['href']=site_url+'/'+fn
    # remove old graph scripts
    for x in soup.find_all('script',attrs={'type':'application/ld+json'}): x.decompose()
    graph=[org,local,{'@type':'Service','@id':site_url+'/'+fn+'#service','name':data['name'],'serviceType':data['name'],'provider':{'@id':site_url+'/#organization'},'areaServed':{'@type':'City','name':'Rajkot'},'description':data['desc'],'url':site_url+'/'+fn}, {'@type':'WebPage','url':site_url+'/'+fn,'name':data['title'],'isPartOf':{'@id':site_url+'/#website'}}, {'@type':'BreadcrumbList','itemListElement':[{'@type':'ListItem','position':1,'name':'Home','item':site_url+'/index.html'},{'@type':'ListItem','position':2,'name':'Services','item':site_url+'/services.html'},{'@type':'ListItem','position':3,'name':data['name'],'item':site_url+'/'+fn}]}]
    sc=soup.new_tag('script',type='application/ld+json'); sc.string=json.dumps({'@context':'https://schema.org','@graph':graph},separators=(',',':')); soup.head.append(sc)
    for prop,content in [('og:title',data['title']),('og:description',data['desc']),('og:type','website'),('og:url',site_url+'/'+fn),('og:site_name',brand)]:
        t=soup.find('meta',attrs={'property':prop}); t['content']=content if t else None
        if not t:
            t=soup.new_tag('meta',attrs={'property':prop,'content':content}); soup.head.append(t)
    # main
    main=soup.new_tag('main')
    hero=soup.new_tag('section',attrs={'class':'pageHero'}); c=soup.new_tag('div',attrs={'class':'container reveal'}); 
    label=soup.new_tag('div',attrs={'class':'mono red pageLabel'}); label.string=data['tag']; c.append(label)
    h=soup.new_tag('h1'); h.string=data['name']+' in '; sp=soup.new_tag('span',attrs={'class':'red'}); sp.string='Rajkot, Gujarat'; h.append(sp); c.append(h)
    p=soup.new_tag('p'); p.string=data['desc']; c.append(p); hero.append(c); main.append(hero)
    sec=soup.new_tag('section'); cont=soup.new_tag('div',attrs={'class':'container seoArticle'}); 
    intro=soup.new_tag('div',attrs={'class':'sectionHead reveal'}); left=soup.new_tag('div'); lab=soup.new_tag('div',attrs={'class':'mono red'}); lab.string='CODETWIN / '+data['tag'].split(' / ')[-1]; left.append(lab); hh=soup.new_tag('h2'); hh.string=data['keyword']; left.append(hh); intro.append(left); sec.append(intro)
    for title,text in data['paras']:
        art=soup.new_tag('article',attrs={'class':'seoBlock reveal'}); h3=soup.new_tag('h3'); h3.string=title; art.append(h3); pp=soup.new_tag('p'); pp.string=text; art.append(pp); cont.append(art)
    # CTA links
    cta=soup.new_tag('div',attrs={'class':'seoCta'}); cp=soup.new_tag('p'); cp.string='Ready to discuss your project in Rajkot?'; cta.append(cp)
    for href,label in [('contact.html','Request a Service ↗'),('services.html','View All Services ↗')]:
        a=soup.new_tag('a',href=href,attrs={'class':'btn red' if href=='contact.html' else 'btn dark'}); a.string=label; cta.append(a)
    cont.append(cta); sec.append(cont); main.append(sec)
    soup.body.main.replace_with(main)
    # extra style
    st=soup.new_tag('style'); st.string='.seoArticle{max-width:920px}.seoArticle .sectionHead{margin-bottom:35px}.seoArticle .sectionHead h2{font-size:clamp(42px,6vw,72px)}.seoBlock{padding:30px 0;border-top:1px solid var(--line)}.seoBlock h3{font-size:28px;letter-spacing:-.03em;margin:0 0 12px}.seoBlock p{font-size:16px;line-height:1.9;color:#999;margin:0;max-width:820px}.seoCta{margin-top:30px;padding:30px;border:1px solid var(--line);display:flex;align-items:center;justify-content:space-between;gap:18px;flex-wrap:wrap}.seoCta p{margin:0;color:#aaa}'
    soup.head.append(st)
    add_blog_nav(soup); ensure_alt(soup)
    (root/fn).write_text(str(soup),encoding='utf8')

# Blog pages
blogs={
'blog.html':('Digital Growth Blog | CodeTwin Technology','Practical articles from CodeTwin Technology about websites, mobile apps, custom software, UI/UX and digital marketing in Rajkot, Gujarat.'),
'blog-website-development-rajkot.html':('Website Development in Rajkot: What a Business Website Should Do','A practical guide to planning a business website in Rajkot, Gujarat, including structure, responsive design, enquiries, SEO foundations and integrations.'),
'blog-mobile-app-development.html':('Mobile App Development: From Idea to Launch','A practical overview of mobile app development, user flows, UI/UX, APIs, testing and launch planning for businesses.'),
'blog-digital-marketing-company.html':('Digital Marketing Company in Rajkot: Building a Connected Customer Journey','How websites, Google Ads, Meta Ads, landing pages and measurement can work together for a local business.'),
}
blog_articles={
'blog-website-development-rajkot.html':[
('Start with the business goal','A useful website begins with a business goal. That might be generating enquiries, explaining services, selling products, collecting bookings or giving customers a reliable place to learn about the company. Before choosing layouts, list the actions that matter and the information customers need to make those actions.'),
('Build for mobile first experiences','Many visitors will discover a local business on a phone. Navigation, buttons, forms, images and text should remain comfortable on smaller screens. Responsive design should adapt the layout rather than simply shrinking a desktop page.'),
('Create clear service and contact paths','A visitor should quickly understand what the business offers and how to take the next step. Dedicated service sections, useful calls to action, contact options and internal links can reduce friction. For a Rajkot business, location information should be accurate and relevant to the actual service area.'),
('SEO foundations matter','Each important page should have a useful title, description, one clear H1, descriptive headings, relevant internal links and meaningful image alt text. Structured data can help search engines understand certain business and page types. A sitemap and correctly configured robots.txt also help with crawl discovery.'),
('Connect the website to operations','Forms, WhatsApp, analytics, booking flows, payment systems and APIs can turn a static website into a working business tool. The right integrations depend on the business; they should reduce friction rather than add unnecessary complexity.'),
('Keep improving after launch','A website is not finished when it goes live. New services, customer questions, projects and search topics can become useful pages or articles. Reviewing analytics and enquiries can show which parts of the website deserve improvement next.')],
'blog-mobile-app-development.html':[
('Define the user problem','A mobile app should solve a clear problem for a defined user. Start with the task the user needs to complete, the information they need and the outcome the business wants to achieve.'),
('Map the experience before coding','User flows and wireframes help reveal missing states and unnecessary steps. Figma prototypes can make the product easier to review before development begins.'),
('Plan the backend','Most business apps need APIs, authentication and data storage. Decide early what information is stored, which actions require accounts and how the app communicates with the backend.'),
('Design for real devices','Touch targets, readable typography, loading states, empty states, validation and network conditions all matter. The app should feel practical when used outside a design mockup.'),
('Test the complete journey','Testing should cover the full workflow from opening the app to completing the main action. Check forms, permissions, API errors, notifications and different screen sizes.'),
('Launch in phases','A first release can focus on the most important workflow and leave secondary features for later. This can make it easier to learn from real users and plan the next version.')],
'blog-digital-marketing-company.html':[
('Digital marketing starts with the customer journey','A campaign does not exist separately from the website. A person may see an ad, visit a landing page, compare the offer and then contact the business. Each step should support the next.'),
('Use Google Ads for active search intent','Search advertising can connect businesses with people who are already looking for a service. Campaign structure, ad messaging and landing pages should match the actual service and customer intent.'),
('Use Meta Ads for discovery and lead generation','Facebook and Instagram campaigns can support awareness and lead-generation journeys. Creative, audience and offer should be planned together, with a clear next step after the interaction.'),
('Make landing pages focused','A campaign landing page should answer the visitor’s immediate questions and make the desired action clear. Too many competing messages can make the next step harder to understand.'),
('Measure useful outcomes','Clicks and reach can be useful, but the business also needs to understand enquiries, leads and conversion activity. Measurement should reflect the actual goal of the campaign.'),
('Connect marketing with development','A digital marketing company can be more useful when it understands the website and product behind the campaign. CodeTwin combines development, UI/UX and advertising services so the customer journey can be planned as one connected system.')]
}

for fn,(title,desc) in blogs.items():
    if fn=='blog.html':
        soup=BeautifulSoup((root/'services.html').read_text(encoding='utf8'),'html.parser')
        soup.title.string=title; soup.find('meta',attrs={'name':'description'})['content']=desc
        soup.find('link',attrs={'rel':'canonical'})['href']=site_url+'/'+fn
        for x in soup.find_all('script',attrs={'type':'application/ld+json'}): x.decompose()
        graph=[org,local,{'@type':'WebPage','url':site_url+'/'+fn,'name':title},{'@type':'BreadcrumbList','itemListElement':[{'@type':'ListItem','position':1,'name':'Home','item':site_url+'/index.html'},{'@type':'ListItem','position':2,'name':'Blog','item':site_url+'/'+fn}]}]
        sc=soup.new_tag('script',type='application/ld+json'); sc.string=json.dumps({'@context':'https://schema.org','@graph':graph},separators=(',',':')); soup.head.append(sc)
        main=soup.new_tag('main'); hero=soup.new_tag('section',attrs={'class':'pageHero'}); c=soup.new_tag('div',attrs={'class':'container reveal'}); lab=soup.new_tag('div',attrs={'class':'mono red pageLabel'}); lab.string='08 / BLOG'; c.append(lab); h=soup.new_tag('h1'); h.string='CodeTwin '; sp=soup.new_tag('span',attrs={'class':'red'}); sp.string='Insights'; h.append(sp); c.append(h); p=soup.new_tag('p'); p.string='Practical guides about websites, apps, software and digital marketing for businesses in Rajkot, Gujarat.'; c.append(p); hero.append(c); main.append(hero)
        sec=soup.new_tag('section'); cont=soup.new_tag('div',attrs={'class':'container'}); sh=soup.new_tag('div',attrs={'class':'sectionHead reveal'}); left=soup.new_tag('div'); lb=soup.new_tag('div',attrs={'class':'mono red'}); lb.string='01 / ARTICLES'; left.append(lb); hh=soup.new_tag('h2'); hh.string='Build smarter. Grow with clarity.'; left.append(hh); sh.append(left); cont.append(sh)
        for bfn,bt in [(k,blogs[k][0]) for k in blog_articles]:
            card=soup.new_tag('article',attrs={'class':'serviceCard reveal'}); hh=soup.new_tag('h3'); hh.string=bt; card.append(hh); pp=soup.new_tag('p'); pp.string=blogs[bfn][1]; card.append(pp); a=soup.new_tag('a',href=bfn,attrs={'class':'serviceLearn'}); a.string='Read article ↗'; card.append(a); cont.append(card)
        sec.append(cont); main.append(sec); soup.body.main.replace_with(main)
        st=soup.new_tag('style'); st.string='.serviceCard{border:1px solid var(--line);padding:30px;background:#0b0b0b}.serviceCard h3{font-size:26px;margin:0 0 12px}.serviceCard p{color:#888;line-height:1.7;margin:0}' ; soup.head.append(st)
    else:
        soup=BeautifulSoup((root/'services.html').read_text(encoding='utf8'),'html.parser')
        soup.title.string=title; soup.find('meta',attrs={'name':'description'})['content']=desc; soup.find('link',attrs={'rel':'canonical'})['href']=site_url+'/'+fn
        for x in soup.find_all('script',attrs={'type':'application/ld+json'}): x.decompose()
        article_data={'@type':'Article','headline':title,'description':desc,'author':{'@type':'Organization','name':brand},'publisher':{'@type':'Organization','name':brand,'logo':{'@type':'ImageObject','url':site_url+'/'+logo}},'mainEntityOfPage':site_url+'/'+fn}
        graph=[org,local,article_data,{'@type':'BreadcrumbList','itemListElement':[{'@type':'ListItem','position':1,'name':'Home','item':site_url+'/index.html'},{'@type':'ListItem','position':2,'name':'Blog','item':site_url+'/blog.html'},{'@type':'ListItem','position':3,'name':title,'item':site_url+'/'+fn}]}]
        sc=soup.new_tag('script',type='application/ld+json'); sc.string=json.dumps({'@context':'https://schema.org','@graph':graph},separators=(',',':')); soup.head.append(sc)
        main=soup.new_tag('main'); hero=soup.new_tag('section',attrs={'class':'pageHero'}); c=soup.new_tag('div',attrs={'class':'container reveal'}); lab=soup.new_tag('div',attrs={'class':'mono red pageLabel'}); lab.string='08 / BLOG'; c.append(lab); h=soup.new_tag('h1'); h.string=title; c.append(h); p=soup.new_tag('p'); p.string=desc; c.append(p); hero.append(c); main.append(hero)
        sec=soup.new_tag('section'); cont=soup.new_tag('div',attrs={'class':'container seoArticle'}); sh=soup.new_tag('div',attrs={'class':'sectionHead reveal'}); left=soup.new_tag('div'); lb=soup.new_tag('div',attrs={'class':'mono red'}); lb.string='CODETWIN / GUIDE'; left.append(lb); hh=soup.new_tag('h2'); hh.string=title; left.append(hh); sh.append(left); cont.append(sh)
        for t,tx in blog_articles[fn]:
            art=soup.new_tag('article',attrs={'class':'seoBlock reveal'}); h3=soup.new_tag('h3'); h3.string=t; art.append(h3); pp=soup.new_tag('p'); pp.string=tx; art.append(pp); cont.append(art)
        a=soup.new_tag('a',href='contact.html',attrs={'class':'btn red'}); a.string='Discuss Your Project ↗'; cont.append(a); sec.append(cont); main.append(sec); soup.body.main.replace_with(main)
        st=soup.new_tag('style'); st.string='.seoArticle{max-width:920px}.seoArticle .sectionHead{margin-bottom:35px}.seoBlock{padding:30px 0;border-top:1px solid var(--line)}.seoBlock h3{font-size:28px;margin:0 0 12px}.seoBlock p{font-size:16px;line-height:1.9;color:#999;margin:0;max-width:820px}' ; soup.head.append(st)
    add_blog_nav(soup); ensure_alt(soup)
    soup_path=root/fn; soup_path.write_text(str(soup),encoding='utf8')

# Make all internal links crawlable from nav/footer and add a Services -> detail index links in service cards by label replacement if not already.
# Update existing services page H3s to link via appended serviceLearn created earlier.

# sitemap and robots
urls=['index.html','about.html','services.html','projects.html','contact.html','blog.html']+list(services.keys())+list(blog_articles.keys())
# unique preserving
seen=[]; [seen.append(x) for x in urls if x not in seen]
(root/'sitemap.xml').write_text('<?xml version="1.0" encoding="UTF-8"?>\n<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">\n'+''.join(f'  <url><loc>{site_url}/{u}</loc></url>\n' for u in seen)+'</urlset>\n',encoding='utf8')
(root/'robots.txt').write_text(f'User-agent: *\nAllow: /\nSitemap: {site_url}/sitemap.xml\n',encoding='utf8')
(root/'SEO-SETUP.md').write_text(f'''# CodeTwin Technology SEO setup\n\nThis package preserves the existing black/red CodeTwin theme and adds technical/content SEO.\n\n## Before publishing\n1. Replace `https://YOUR-DOMAIN-HERE.com` in `sitemap.xml`, `robots.txt`, canonical URLs and JSON-LD with the real production domain. The site domain was not supplied, so it is intentionally not guessed.\n2. In Google Search Console, add the real domain/property, complete verification, then submit `/sitemap.xml`. Google recommends submitting a sitemap and using URL Inspection after structured-data deployment.\n3. Add your Google Analytics 4 Measurement ID to the pages. No ID was supplied, so no fake tracking ID was inserted.\n4. Validate structured data with Google's Rich Results Test and inspect the live URLs after deployment.\n\n## Location\nAll local SEO wording uses **Rajkot, Gujarat**, not Surat.\n\n## Added\n- Unique title + meta description per page\n- One H1 per page with page-focused keyword intent\n- Service detail pages with long-form useful content\n- Image alt text coverage\n- Organization + LocalBusiness schema\n- Service schema on service detail pages\n- Breadcrumb schema\n- Blog + Article schema\n- XML sitemap\n- robots.txt\n- Internal links between core pages, service pages and blog articles\n- Blog topics: Website Development in Rajkot, Mobile App Development, Digital Marketing Company in Rajkot\n\n## Important\nSEO improvements do not guarantee a particular ranking or score. Search performance depends on the live domain, content quality, technical performance, competition, links, indexing and Google's systems.\n''',encoding='utf8')

# Verify H1 and titles/descriptions
for p in root.glob('*.html'):
    s=BeautifulSoup(p.read_text(encoding='utf8'),'html.parser')
    assert len(s.find_all('h1'))==1,(p,len(s.find_all('h1')))
    assert s.title and s.title.string
    assert s.find('meta',attrs={'name':'description'})
    for img in s.find_all('img'): assert img.get('alt') is not None
print('HTML SEO verification passed for',len(list(root.glob('*.html'))),'pages')
