from kivy.app import App
from kivy.uix.boxlayout import BoxLayout 
from kivy.uix.button import Button
from kivy.uix.textinput import TextInput
from kivy.uix.label import Label
from kivy.core.window import Window
from kivy.core.audio import SoundLoader
from kivy.clock import Clock



Window.size = (590, 500)
Window.clearcolor = (23/255, 65/255, 147/255, 1)
Window.title = "Ну, подумай"
x = 0
y = 0
total = 0
z = []
class SerApp(App):
    def build(self):
        
        b = BoxLayout(orientation='vertical', spacing=20 )


        label2 = Label(text='Цель игры: Называя по очереди числа от 1 до 10 и суммируя их сделать так,\n'
                       'что бы  ваш ход закончился на 49 и какое бы число не назвал соперник\n  получится 50'
                       'и больше, что будет являться вашим  выйгрышем.\n \n  Для начала игры введите значение'
                       'первым\n либо нажмите на кнопку  первого хода программой',  size_hint=(1, 1), halign='center', valign='middle')
        b.add_widget(label2)
        self.sound = SoundLoader.load('C:\\1na.wav')

        
        t = TextInput(text='', halign='center',  font_size=30, multiline=False)
        t.pos_hint={'x': 0.39, 'y': 0.1}
        t.size_hint_y = 0.3##высота виджета entry
        t.size_hint_x = 0.25 ##ширинf виджета entry
        t.bind(on_text_validate=self.on_enter)
        b.add_widget(t)
        self.t = t
        

##       
        button = Button(text="ход программы", pos_hint={'x': 0.36, 'y': 0.1}, size_hint=(0.3, 0.25), height=28,  on_press=self.num)
        b.add_widget(button)
        self.button = button
        
        


        
        label = Label(text="", pos_hint={'x': 0.36, 'y': 0.1}, size_hint=(0.3, 0.25), valign='top')
        self.label = label
        label3 = Label(text='спонсор разработки сайт Цифра и Аналог', halign='center', font_size=10, valign='middle')
        b.add_widget(label3)
        self.label3 = label3
        label5 = Label(text='спонсор разработки сайт Цифра и Аналог', halign='center', font_size=10, valign='middle')
        self.label5 = label5


        self.sound.play()
        return b
    
    def on_enter(self, instance):
        global y
        y = instance.text
        print(y)
        try:
            y = int(self.t.text)
            if 1<= y <= 11:
                    print('zbs')
                    
                    
            else:
                   print('что то вы ввели не то число') 
##                    label9.config(text='что то вы ввели не то число ')
        except ValueError:
                    print('что то вы ввели вообще не то ')
        
        def set_focus(dt):
            instance.focus = True  # Исправлено на instance.focus
            self.ser3()

        Clock.schedule_once(set_focus, 0.1)
        instance.text = ''
        
    def num(self, instanse):
        print('папапп')
        

    def ser3(self):
            self.root.remove_widget(self.button)
            self.root.remove_widget(self.label3)
            self.root.add_widget(self.label)
            self.root.add_widget(self.label5)
##            self.root.add_widget(self.label6)
##            self.root.add_widget(self.new_label2)

            global y
            global x
            global total
            global z

            if total == 0 and y < 5:
             x = 5 - y
            z.append(x + y)
            total = sum(z)
            
            self.label.text = f'        Ваш ход: {y} \n Ход программы: {x}\n     Сумма чисел:\n               {total}'

     
           

if __name__ == "__main__":
    SerApp().run()
