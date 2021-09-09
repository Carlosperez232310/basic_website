import bs4 as bs
import urllib.request
import ui
from PIL import Image

view=ui.View()
view.background_color='pink'
text=ui.TextView(alignment=True)
view.add_subview(text)
text.frame=45,350,300,60
text.border_color=0.55, 0.55, 1.0
text.border_width=6

close=ui.Button(10,10)
view.add_subview(close)
close.frame=20,40,40,40
close.title='X'
close.background_color=1.0, 0.81, 0.86
close.tint_color=0.5, 0.5, 0.5

summary=ui.Button(600,600)
view.add_subview(summary)
summary.background_color=0.95, 0.66, 1.0
summary.frame=100,150,200,50
summary.title='Summary'

search=ui.Button(600,600)
view.add_subview(search)
search.background_color=0.95, 0.66, 1.0
search.frame=100,250,200,50
search.title='Search'

def abutton_tapped(self):
	search_view=ui.TextView(editable=False)
	
	search_view.background_color='white'
	S2=text.text
	source = urllib.request.urlopen('https://en.m.wikipedia.org/wiki/'+S2).read()
	soup = bs.BeautifulSoup(source,'html.parser')
	
	for p in soup.find_all('p'):
		for b in p.find_all('b'):
			ps=p.text
	search_view.text=ps
	search_view.present('fullscreen')

def sbutton_tapped(self):
	search_view=ui.TextView(editable=False)
	
	search_view.background_color='white'
	S2=text.text
	source = urllib.request.urlopen('https://en.m.wikipedia.org/wiki/'+S2).read()
	soup = bs.BeautifulSoup(source,'html.parser')
	
	search_view.text=soup.text
	search_view.present('fullscreen')
	
	
def Xbutton_tapped(self):
	view.close()
	
	
summary.action=abutton_tapped
search.action=sbutton_tapped	


#print(soup.find_all('p'))

#for paragraph in soup.find_all('p'):
	#print(paragraph.string)
	#print(str(paragraph.text))

close.action=Xbutton_tapped
view.present('fullscreen',hide_title_bar=True)
