import keyboard
import time
import logging
from datetime import datetime
import pyperclip

# Настройка логгера
logging.basicConfig(
    filename='forward.log',
    level=logging.INFO,
    format='%(asctime)s - %(message)s',
    datefmt='%Y-%m-%d %H:%M:%S'
)

def log_action(action):
    """Логирует действие и выводит его в консоль"""
    logging.info(action)
    print(f"[{datetime.now().strftime('%H:%M:%S')}] {action}")

def switch_layout():
    keyboard.press('ctrl')
    keyboard.press('shift')
    keyboard.release('shift')
    keyboard.release('ctrl')
    time.sleep(0.3)

def clear_text():
    keyboard.press('ctrl')
    keyboard.press('a')
    keyboard.release('a')
    keyboard.release('ctrl')
    time.sleep(0.2)
    keyboard.press('delete')
    keyboard.release('delete')
    time.sleep(0.2)
    log_action("Текст очищен")

def copy_text():
    keyboard.press('ctrl')
    keyboard.press('c')
    keyboard.release('c')
    keyboard.release('ctrl')
    time.sleep(0.5)
    
    log_action("Текст скопирован")

def paste_text():
    keyboard.press('ctrl')
    keyboard.press('v')
    keyboard.release('v')
    keyboard.release('ctrl')
    time.sleep(0.2)
    log_action("Текст вставлен")
    

def main():
    print("Готов к работе. Нажмите:")
    print("Delete - очистить текст")
    print("Home - копировать (Ctrl+C)")
    print("End - вставить (Ctrl+V)")
    print("Escape - выход")
    log_action("Программа запущена")
    
    while True:
        if keyboard.is_pressed('home'):
            switch_layout()
            switch_layout()
            copy_text()
            switch_layout()
            time.sleep(0.2)
            
        if keyboard.is_pressed('end'):
            switch_layout()
            paste_text()
            switch_layout()
            time.sleep(0.2)
            
        if keyboard.is_pressed('delete'):
            switch_layout()
            clear_text()
            switch_layout()
            time.sleep(0.2)
            
        if keyboard.is_pressed('esc'):
            log_action("Программа завершена")
            print("Выход")
            break

if __name__ == "__main__":
    keyboard.add_hotkey('delete', lambda: None)
    keyboard.add_hotkey('home', lambda: None)
    keyboard.add_hotkey('end', lambda: None)
    keyboard.add_hotkey('esc', lambda: None)
    main()
