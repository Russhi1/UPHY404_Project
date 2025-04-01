# UPHY404_Project
## Implementation of a Full Adder Circuit 

### Code
```
import sys
from PyQt5.QtWidgets import (QApplication, QWidget, QLabel, QLineEdit,
                             QPushButton, QVBoxLayout, QHBoxLayout, QGridLayout,
                             QGraphicsScene, QGraphicsView, QGraphicsRectItem,
                             QGraphicsLineItem, QGraphicsTextItem)
from PyQt5.QtGui import QPen, QColor, QFont
from PyQt5.QtCore import Qt

def full_adder(a, b, carry_in):
    """Simulates a full adder circuit."""
    sum_bit = a ^ b ^ carry_in
    carry_out = (a & b) | (carry_in & (a ^ b))
    return sum_bit, carry_out

class FullAdderGUI(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()

    def initUI(self):
        self.setWindowTitle("Full Adder Simulator")
        self.setGeometry(100, 100, 400, 300)

        # Input fields
        self.label_a = QLabel("Input A (0 or 1):")
        self.entry_a = QLineEdit()
        self.label_b = QLabel("Input B (0 or 1):")
        self.entry_b = QLineEdit()
        self.label_carry_in = QLabel("Carry-in (0 or 1):")
        self.entry_carry_in = QLineEdit()

        # Calculate button
        self.calculate_button = QPushButton("Calculate and Update")
        self.calculate_button.clicked.connect(self.calculate_and_update)

        # Graphics scene and view
        self.scene = QGraphicsScene()
        self.view = QGraphicsView(self.scene)
        self.view.setAlignment(Qt.AlignLeft | Qt.AlignTop)

        # Layout
        input_layout = QGridLayout()
        input_layout.addWidget(self.label_a, 0, 0)
        input_layout.addWidget(self.entry_a, 0, 1)
        input_layout.addWidget(self.label_b, 1, 0)
        input_layout.addWidget(self.entry_b, 1, 1)
        input_layout.addWidget(self.label_carry_in, 2, 0)
        input_layout.addWidget(self.entry_carry_in, 2, 1)

        main_layout = QVBoxLayout()
        main_layout.addLayout(input_layout)
        main_layout.addWidget(self.calculate_button)
        main_layout.addWidget(self.view)

        self.setLayout(main_layout)
        self.draw_full_adder_circuit()
        self.show()

    def draw_full_adder_circuit(self):
        """Draws the full adder circuit on the scene."""
        x, y = 50, 50
        self.rect = QGraphicsRectItem(x, y, 100, 80)
        self.scene.addItem(self.rect)
        text = QGraphicsTextItem("Full Adder")
        text.setPos(x + 25, y + 25)
        self.scene.addItem(text)

        self.line_a = QGraphicsLineItem(x - 30, y + 15, x, y + 15)
        self.scene.addItem(self.line_a)
        text_a = QGraphicsTextItem("A")
        text_a.setPos(x - 45, y + 5)
        self.scene.addItem(text_a)

        self.line_b = QGraphicsLineItem(x - 30, y + 40, x, y + 40)
        self.scene.addItem(self.line_b)
        text_b = QGraphicsTextItem("B")
        text_b.setPos(x - 45, y + 30)
        self.scene.addItem(text_b)

        self.line_cin = QGraphicsLineItem(x - 30, y + 65, x, y + 65)
        self.scene.addItem(self.line_cin)
        text_cin = QGraphicsTextItem("Cin")
        text_cin.setPos(x - 45, y + 55)
        self.scene.addItem(text_cin)

        self.line_sum = QGraphicsLineItem(x + 100, y + 25, x + 130, y + 25)
        self.scene.addItem(self.line_sum)
        text_sum = QGraphicsTextItem("Sum")
        text_sum.setPos(x + 135, y + 15)
        self.scene.addItem(text_sum)

        self.line_cout = QGraphicsLineItem(x + 100, y + 55, x + 130, y + 55)
        self.scene.addItem(self.line_cout)
        text_cout = QGraphicsTextItem("Cout")
        text_cout.setPos(x + 135, y + 45)
        self.scene.addItem(text_cout)

    def update_values(self, a, b, carry_in, sum_bit, carry_out):
        """Updates the input/output values and line colors."""
        pen_red = QPen(QColor("red"))
        pen_black = QPen(QColor("black"))

        self.line_a.setPen(pen_red if a == 1 else pen_black)
        self.line_b.setPen(pen_red if b == 1 else pen_black)
        self.line_cin.setPen(pen_red if carry_in == 1 else pen_black)
        self.line_sum.setPen(pen_red if sum_bit == 1 else pen_black)
        self.line_cout.setPen(pen_red if carry_out == 1 else pen_black)

        text_values = QGraphicsTextItem(f"A={a}, B={b}, Cin={carry_in}\nSum={sum_bit}, Cout={carry_out}")
        text_values.setPos(50, 150)
        self.scene.addItem(text_values)

    def calculate_and_update(self):
        """Calculates and updates the full adder values and line colors."""
        try:
            a = int(self.entry_a.text())
            b = int(self.entry_b.text())
            carry_in = int(self.entry_carry_in.text())

            if a not in (0, 1) or b not in (0, 1) or carry_in not in (0, 1):
                raise ValueError("Inputs must be 0 or 1.")

            sum_bit, carry_out = full_adder(a, b, carry_in)
            self.update_values(a, b, carry_in, sum_bit, carry_out)

        except ValueError as e:
            print(f"Error: {e}")
        except Exception as e:
            print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    app = QApplication(sys.argv)
    gui = FullAdderGUI()
    sys.exit(app.exec_())
```

## Demo 

![image](https://github.com/user-attachments/assets/016eff6b-1ee0-4c4f-847c-cc5d2a0fe441)

