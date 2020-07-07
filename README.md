# Web-Scrapping
Scrapping Emails with corresponding Name
%%time
journal_name_address_vaccines = {}
for journal_name,links in dict_journal_link.items():
    name_address = {}
    for link in links:
        try:
            link = Request(link,headers={"User-Agent": "Mozilla/5.0"})
            open_link = url.urlopen(link).read()
            soup_link = bs(open_link,'lxml')
            name_surname = soup_link.find_all('a',{'class':"author size-m workspace-trigger"})
            
            for index, value in enumerate(name_surname):
                if value.find_all('path') !=[]:
                    full_name = name+surname
                    full_name=' '.join(full_name)
            address = re.findall(r"[a-zA-Z0-9._-]+@[a-zA-Z0-9._-]+\.[a-zA-Z0-9_-a-z]+[a-zA-Z0-9_-a-z]",soup_link.text)
            print(journal_name,full_name,address)
            if len(address)>0:
                name_address[full_name] = address
        except:
            continue
    journal_name_address_vaccines[journal_name] = name_address 
    --------------------------------------------------------   
      dict_journal_link = {}
  link_plus_pdf = {}
  for article_name,link in link_journal.items():
      link = Request(link,headers={"User-Agent": "Mozilla/5.0"})
      open_article = url.urlopen(link).read()
      soup_article = bs(open_article, 'lxml')
      lst_page_number = [*,*]
      append_links = []
      print(lst_page_number[1])
      if lst_page_number[1] > 25:
          for number in range(lst_page_number[0],lst_page_number[1]):
              name_article = ('+').join(article_name.split())
              if len(append_links) < ****:
                  if number > 1:
                      print(number)
                      next_page_link = Request('https://www.website.com/='+str(number), 
                        headers={"User-Agent": "Mozilla/5.0"})
                      next_open_article =  url.urlopen(next_page_link).read()
                      next_soup_article = bs(next_open_article,'lxml')
                      next_list_links = next_soup_article.find_all('a',{'class':'result-list-title-link u-font-serif text-s'})
                      print(len(next_list_links))
                      for link in next_list_links:
                          append_links.append('https://www.website.com'+link['href'])
                  else:#for the first page     
                      list_links = soup_article.find_all('a',{'class':'result-list-title-link u-font-serif text-s'})
                      for link in list_links:
                          append_links.append('https://www.website.com'+link['href'])
              else:
                  break
          dict_journal_link[article_name] = append_links
