import win32api, win32con
from random import randint
from win32api import GetSystemMetrics
import threading

def click():
	temp_int = randint(0, 30)
	if temp_int<5 : 
		return
	screen_width = 	GetSystemMetrics(0)
	screen_height = GetSystemMetrics(1)
	x = randint(0, screen_width)
	y = randint(0, screen_height)
	win32api.SetCursorPos((x,y))
	win32api.mouse_event(win32con.MOUSEEVENTF_LEFTDOWN,x,y,0,0)
	win32api.mouse_event(win32con.MOUSEEVENTF_LEFTUP,x,y,0,0)
	
def set_interval(func, sec=5):
	def func_wrapper():
		# set_interval(func, sec)
		if not func():
			set_interval(func, sec)
	t = threading.Timer(sec, func_wrapper)
	t.start()
	return t

if __name__ == '__main__':
	set_interval(click, sec=10)
  
  
  
  
from cx_Freeze import setup, Executable

base = None    

executables = [Executable("mouse.py", base=base)]

packages = ["idna","win32api","win32con","random","win32api","threading"]
options = {
    'build_exe': {    
        'packages':packages,
    },    
}

setup(
    name = "auto_mouse",
    options = options,
    version = "0.1",
    description = 'auto mouse move and click',
    executables = executables
)
