# web-browser
The objective of this  Python project is to create a GUI based  Web Browser. To build this, you must have intermediate understanding of the  PyQt5 library, and its modules, including the WebEngineWidgets module that you will need to install separately.
#Creating a Simple Web Browser with Python and PyQT
#Project Prerequisites:
1.  PyQt5 – To create the GUI.
2. sys.argv – To get the inputs entered from the command line
3. PyQt5.QtCore.QUrl – The QUrl class will be used to convert string objects to a Qt acceptable URL object that will navigate through all the websites.
4. PyQt5.QtWidgets – To get the Widgets, including but not limited to:
a. QAction – This widget allots an abstract user interface action to widgets in the form of text.
b. QLineEdit – Single line input box [Tkinter alternative: Entry widget]
c. QToolbar – This widget is used to add a frame-like container to the top of the window.
5.  PyQt5.QtWebEngineWidgets.QWebEngineView – It is used to load the content of a website directly from the internet.
6.  import sys.argv as argv 

from PyQt5.QtCore import QUrl
from PyQt5.QtWebEngineWidgets import QWebEngineView
#                                 Web Browser (HTML Frame)
from PyQt5.QtWidgets import *

class Window(QMainWindow):
  def __init__(self, *args, **kwargs):
     super(Window, self).__init__(*args, **kwargs)
     
     self.browser = QWebEngineView()
     self.browser.setUrl(QUrl('https://www.google.com'))
     self.browser.urlChanged.connect(self.update_AddressBar)
     self.setCentralWidget(self.browser)

     self.status_bar = QStatusBar()
     self.setStatusBar(self.status_bar)

     self.navigation_bar = QToolBar('Navigation Toolbar')
     self.addToolBar(self.navigation_bar)

     back_button = QAction("Back", self)
     back_button.setStatusTip('Go to previous page you visited')
     back_button.triggered.connect(self.browser.back)
     self.navigation_bar.addAction(back_button)

     refresh_button = QAction("Refresh", self)
     refresh_button.setStatusTip('Refresh this page')
     refresh_button.triggered.connect(self.browser.reload)
     self.navigation_bar.addAction(refresh_button)


     next_button = QAction("Next", self)
     next_button.setStatusTip('Go to next page')
     next_button.triggered.connect(self.browser.forward)
     self.navigation_bar.addAction(next_button)

     home_button = QAction("Home", self)
     home_button.setStatusTip('Go to home page (Google page)')
     home_button.triggered.connect(self.go_to_home)
     self.navigation_bar.addAction(home_button)

     self.navigation_bar.addSeparator()

     self.URLBar = QLineEdit()
     self.URLBar.returnPressed.connect(lambda: self.go_to_URL(QUrl(self.URLBar.text())))  # This specifies what to do when enter is pressed in the Entry field
     self.navigation_bar.addWidget(self.URLBar)

     self.addToolBarBreak()

     # Adding another toolbar which contains the bookmarks
     bookmarks_toolbar = QToolBar('Bookmarks', self)
     self.addToolBar(bookmarks_toolbar)

     pythongeeks = QAction("PythonGeeks", self)
     pythongeeks.setStatusTip("Go to PythonGeeks website")
     pythongeeks.triggered.connect(lambda: self.go_to_URL(QUrl("https://pythongeeks.org")))
     bookmarks_toolbar.addAction(pythongeeks)

     facebook = QAction("Facebook", self)
     facebook.setStatusTip("Go to Facebook")
     facebook.triggered.connect(lambda: self.go_to_URL(QUrl("https://www.facebook.com")))
     bookmarks_toolbar.addAction(facebook)

     linkedin = QAction("LinkedIn", self)
     linkedin.setStatusTip("Go to LinkedIn")
     linkedin.triggered.connect(lambda: self.go_to_URL(QUrl("https://in.linkedin.com")))
     bookmarks_toolbar.addAction(linkedin)

     instagram = QAction("Instagram", self)
     instagram.setStatusTip("Go to Instagram")
     instagram.triggered.connect(lambda: self.go_to_URL(QUrl("https://www.instagram.com")))
     bookmarks_toolbar.addAction(instagram)

     twitter = QAction("Twitter", self)
     twitter.setStatusTip('Go to Twitter')
     twitter.triggered.connect(lambda: self.go_to_URL(QUrl("https://www.twitter.com")))
     bookmarks_toolbar.addAction(twitter)

     self.show()

  def go_to_home(self):
     self.browser.setUrl(QUrl('https://www.google.com/'))

  def go_to_URL(self, url: QUrl):
     if url.scheme() == '':
        url.setScheme('https://')
     self.browser.setUrl(url)
     self.update_AddressBar(url)

  def update_AddressBar(self, url):
     self.URLBar.setText(url.toString())
     self.URLBar.setCursorPosition(0)


app = QApplication(argv)
app.setApplicationName('PythonGeeks Web Browser')

window = Window()
app.exec_()
#Explanation:

We start off by creating a Window class inherited from the QMainWindow class of the  PyQt5 library.
In the __init__() function, we give it all the methods, attributes of the Window class, which in turn has functions from its parent class.
Then, we go on creating the layout of the window.
Firstly, we go about setting the details of the QWebEngineView object, including its position in the main window, its initial URL, how to change the URL and the Address bar, and setting its status bar.
Then we create 2 toolbars. Add them to the window, add widgets in them and set them in two different lines.
The navigation_bar toolbar has the back, reload, home action buttons and the address bar.
The bookmarks_toolbar contains bookmarks of the websites that you want to set as bookmarks.
To add 2 toolbars in 2 separate rows, you need to use the QMainWindow.addToolBarbreak() method to add a separator that separates the two toolbars.
The QtWidgets.QAction() function is used to add a special kind of button where each command is represented as an action, which will represent our bookmarks.
The go_to_home() method is used to set the URL of the  browser back to the google homepage, which is our homepage as well.
The go_to_URL() method, which takes one QUrl object as argument, is used to change the URL of the  browser and in the address bar. In case the URL does not have a ‘http://’ or ‘https://’ prefix, the function will add it and then move forward with it.
To activate this method and search your URL, press the enter key on your keyboard.
The update_AddressBar() method is used to set the text of our address bar to the string version of the URL on the browser.
After creating the Window class, we will create a QApplication object, which will essentially run our window.
The QApplication.exec_() is used to run the application.
#Python Web Browser Output
![image](https://github.com/RAGHAVRANA74/web-browser/assets/174944527/d4169070-54b7-4022-9596-69a32be8f5db)
