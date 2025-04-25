# GUI-CALCULATOR-

import tkinter as tk

class Calculator:
    def __init__(self, master):
        self.master = master
        master.title("Calculator")

        self.expression = ""
        self.equation = tk.StringVar()
        self.equation.set("0")

        self.entry = tk.Entry(master, textvariable=self.equation, width=25, font=('Arial', 16), bd=5, relief=tk.SUNKEN, justify='right')
        self.entry.grid(row=0, column=0, columnspan=4, padx=5, pady=5)

        buttons = [
            ("7", 1, 0), ("8", 1, 1), ("9", 1, 2), ("/", 1, 3),
            ("4", 2, 0), ("5", 2, 1), ("6", 2, 2), ("*", 2, 3),
            ("1", 3, 0), ("2", 3, 1), ("3", 3, 2), ("-", 3, 3),
            ("0", 4, 0), (".", 4, 1), ("=", 4, 2), ("+", 4, 3),
            ("C", 5, 0), ("(", 5, 1), (")", 5, 2)
        ]

        for (text, row, col) in buttons:
            button = tk.Button(master, text=text, padx=20, pady=20, font=('Arial', 14),
                                command=lambda t=text: self.button_click(t))
            button.grid(row=row, column=col, padx=2, pady=2, sticky="nsew")
            master.grid_columnconfigure(col, weight=1)
            master.grid_rowconfigure(row, weight=1)

        master.grid_columnconfigure(0, weight=1)
        master.grid_columnconfigure(1, weight=1)
        master.grid_columnconfigure(2, weight=1)
        master.grid_columnconfigure(3, weight=1)
        master.grid_rowconfigure(1, weight=1)
        master.grid_rowconfigure(2, weight=1)
        master.grid_rowconfigure(3, weight=1)
        master.grid_rowconfigure(4, weight=1)
        master.grid_rowconfigure(5, weight=1)

    def button_click(self, text):
        if text == "=":
            try:
                result = eval(self.expression)
                self.equation.set(result)
                self.expression = str(result)
            except Exception as e:
                self.equation.set("Error")
                self.expression = ""
        elif text == "C":
            self.expression = ""
            self.equation.set("0")
        else:
            self.expression += text
            self.equation.set(self.expression)

root = tk.Tk()
calculator = Calculator(root)
root.mainloop()
