# Design Patterns

## **Creational Patterns:**

### 1. **Singleton Pattern**:
   - **Definition**: Ensures that a class has only one instance and provides a global point of access to that instance.
   - **Real-World Analogy**: A president's office with a single president who manages the country.
   - **When to Use**: Use it when you want to ensure that there's only one instance of a class in your application.
   - **Code Example**:
     ```python
     class President:
         _instance = None

         def __new__(cls):
             if cls._instance is None:
                 cls._instance = super(President, cls).__new__(cls)
             return cls._instance

     president1 = President()
     president2 = President()

     print(president1 is president2)  # True, they are the same instance
     ```

### 2. **Factory Method Pattern**:
   - **Definition**: Defines an interface for creating an object but allows subclasses to alter the type of objects that will be created.
   - **Real-World Analogy**: A car factory that produces cars of different models based on customer demand.
   - **When to Use**: Use it when you want to delegate the responsibility of object creation to subclasses.
   - **Code Example**:
     ```python
     class Car:
         def __init__(self, model):
             self.model = model

     class CarFactory:
         @staticmethod
         def create_car(model):
             return Car(model)

     car1 = CarFactory.create_car("SUV")
     car2 = CarFactory.create_car("Sedan")
     ```

### 3. **Abstract Factory Pattern**:
   - **Definition**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
   - **Real-World Analogy**: A furniture factory that produces sets of matching furniture (e.g., table, chairs, and cabinet).
   - **When to Use**: Use it when you need to create families of related objects.
   - **Code Example**:
     ```python
     class Chair:
         pass

     class Table:
         pass

     class FurnitureFactory:
         def create_chair(self):
             pass

         def create_table(self):
             pass

     class ModernFurnitureFactory(FurnitureFactory):
         def create_chair(self):
             return Chair()

         def create_table(self):
             return Table()

     factory = ModernFurnitureFactory()
     chair = factory.create_chair()
     table = factory.create_table()
     ```

### 4. **Builder Pattern**:
   - **Definition**: Separates the construction of a complex object from its representation, allowing the same construction process to create different representations.
   - **Real-World Analogy**: A chef building a custom sandwich based on the customer's choice of bread, filling, and toppings.
   - **When to Use**: Use it when you need to create complex objects with many optional components.
   - **Code Example**:
     ```python
     class Sandwich:
         def __init__(self):
             self.bread = None
             self.fillings = []
             self.toppings = []

     class SandwichBuilder:
         def __init__(self):
             self.sandwich = Sandwich()

         def add_bread(self, bread):
             self.sandwich.bread = bread

         def add_filling(self, filling):
             self.sandwich.fillings.append(filling)

         def add_topping(self, topping):
             self.sandwich.toppings.append(topping)

         def build(self):
             return self.sandwich

     builder = SandwichBuilder()
     builder.add_bread("Wheat")
     builder.add_filling("Turkey")
     builder.add_topping("Lettuce")
     sandwich = builder.build()
     ```

### 5. **Prototype Pattern**:
   - **Definition**: Creates new objects by copying an existing object, known as the prototype.
   - **Real-World Analogy**: A photocopier that duplicates documents based on an original.
   - **When to Use**: Use it when you want to create new objects by copying an existing one, especially when the cost of creating an object is expensive.
   - **Code Example**:
     ```python
     import copy

     class Prototype:
         def clone(self):
             return copy.deepcopy(self)

     class ConcretePrototype(Prototype):
         def __init__(self, data):
             self.data = data

     original = ConcretePrototype("Original Data")
     clone1 = original.clone()
     clone2 = original.clone()
     ```

## **Structural Patterns:**

### 1. **Adapter Pattern**:
   - **Definition**: Allows the interface of an existing class to be used as another interface.
   - **Real-World Analogy**: Using an adapter to plug a European device into a US power socket.
   - **When to Use**: Use it when you need to make two incompatible interfaces work together.
   - **Code Example**:
     ```python
     class EuropeanDevice:
         def plug_in_european_socket(self):
             print("Plugged into European socket")

     class USAdapter:
         def __init__(self, european_device):
             self.european_device = european_device

         def plug_in_us_socket(self):
             print("Plugged into US socket")
             self.european_device.plug_in_european_socket()

     european_device = EuropeanDevice()
     adapter = USAdapter(european_device)
     adapter.plug_in_us_socket()

     # Output:
     # Plugged into US socket
     # Plugged into European socket
     ```

### 2. **Bridge Pattern**:
   - **Definition**: Separates an object's abstraction from its implementation, allowing them to vary independently.
   - **Real-World Analogy**: A remote control that operates various devices like TVs and DVD players.
   - **When to Use**: Use it when you want to avoid a permanent binding between an abstraction and its implementation.
   - **Code Example**:
     ```python
     class Device:
         def turn_on(self):
             pass

         def turn_off(self):
             pass

     class RemoteControl:
         def __init__(self, device):
             self.device = device

         def power_on(self):
             self.device.turn_on()

         def power_off(self):
             self.device.turn_off()

     class TV(Device):
         def turn_on(self):
             print("TV is on")

         def turn_off(self):
             print("TV is off")

     class DVDPlayer(Device):
         def turn_on(self):
             print("DVD Player is on")

         def turn_off(self):
             print("DVD Player is off")

     tv = TV()
     remote = RemoteControl(tv)
     remote.power_on()
     remote.power_off()
     ```

### 3. **Composite Pattern**:
   - **Definition**: Composes objects into tree structures to represent part-whole hierarchies.
   - **Real-World Analogy**: A folder in a computer's file system containing files and subfolders.
   - **When to Use**: Use it when you need to treat individual objects and compositions of objects uniformly.
   - **Code Example**:
     ```python
     class Graphic:
         def draw(self):
             pass

     class CompositeGraphic(Graphic):
         def __init__(self):
             self.graphics = []

         def add(self

, graphic):
             self.graphics.append(graphic)

         def draw(self):
             for graphic in self.graphics:
                 graphic.draw()

     class Circle(Graphic):
         def draw(self):
             print("Drawing a circle")

     class Square(Graphic):
         def draw(self):
             print("Drawing a square")

     circle = Circle()
     square = Square()
     composite = CompositeGraphic()
     composite.add(circle)
     composite.add(square)
     composite.draw()
     ```

### 4. **Decorator Pattern**:
   - **Definition**: Attaches additional responsibilities to an object dynamically, providing a flexible alternative to subclassing.
   - **Real-World Analogy**: Adding toppings to a pizza or filters to an image editor.
   - **When to Use**: Use it when you want to add behavior to individual objects without affecting other objects of the same class.
   - **Code Example**:
     ```python
     class Coffee:
         def cost(self):
             return 5

     class MilkDecorator:
         def __init__(self, coffee):
             self._coffee = coffee

         def cost(self):
             return self._coffee.cost() + 2

     class SugarDecorator:
         def __init__(self, coffee):
             self._coffee = coffee

         def cost(self):
             return self._coffee.cost() + 1

     coffee = Coffee()
     coffee_with_milk = MilkDecorator(coffee)
     coffee_with_sugar = SugarDecorator(coffee)

     print(coffee_with_milk.cost())   # Output: 7
     print(coffee_with_sugar.cost())  # Output: 6
     ```

### 5. **Facade Pattern**:
   - **Definition**: Provides a simplified interface to a complex subsystem, making it easier to use.
   - **Real-World Analogy**: Using a smartphone with a user-friendly touchscreen instead of directly dealing with internal components.
   - **When to Use**: Use it when you want to hide the complexity of a subsystem and provide a simpler interface to clients.
   - **Code Example**:
     ```python
     class SubsystemA:
         def operation_a(self):
             print("Subsystem A: Operation A")

     class SubsystemB:
         def operation_b(self):
             print("Subsystem B: Operation B")

     class Facade:
         def __init__(self):
             self.subsystem_a = SubsystemA()
             self.subsystem_b = SubsystemB()

         def operation(self):
             self.subsystem_a.operation_a()
             self.subsystem_b.operation_b()

     facade = Facade()
     facade.operation()

     # Output:
     # Subsystem A: Operation A
     # Subsystem B: Operation B
     ```

### 6. **Flyweight Pattern**:
   - **Definition**: Minimizes memory usage or computational expenses by sharing as much as possible with similar objects.
   - **Real-World Analogy**: Recycling objects like keys in a piano to save resources.
   - **When to Use**: Use it when you need to create a large number of similar objects efficiently.
   - **Code Example**:
     ```python
     class TreeType:
         def __init__(self, name, color):
             self.name = name
             self.color = color

         def render(self, x, y):
             print(f"Render a {self.color} {self.name} tree at ({x}, {y})")

     class TreeFactory:
         _tree_types = {}

         @staticmethod
         def get_tree_type(name, color):
             if (tree_type := TreeFactory._tree_types.get(name)) is None:
                 tree_type = TreeType(name, color)
                 TreeFactory._tree_types[name] = tree_type
             return tree_type

     class Forest:
         def __init__(self):
             self.trees = []

         def plant_tree(self, x, y, name, color):
             tree_type = TreeFactory.get_tree_type(name, color)
             tree = {"x": x, "y": y, "type": tree_type}
             self.trees.append(tree)

         def draw(self):
             for tree in self.trees:
                 tree["type"].render(tree["x"], tree["y"])

     forest = Forest()
     forest.plant_tree(1, 2, "Maple", "Red")
     forest.plant_tree(3, 4, "Oak", "Green")
     forest.draw()
     ```

## **Behavioral Patterns:**

### 1. **Observer Pattern**:
   - **Definition**: Defines a one-to-many dependency between objects, so when one object changes state, all its dependents are notified and updated automatically.
   - **Real-World Analogy**: Subscribing to a YouTube channel to receive notifications of new videos.
   - **When to Use**: Use it when one object needs to notify multiple objects about changes without knowing who or what those objects are.
   - **Code Example**:
     ```python
     class Subject:
         def __init__(self):
             self._observers = []

         def attach(self, observer):
             self._observers.append(observer)

         def detach(self, observer):
             self._observers.remove(observer)

         def notify(self):
             for observer in self._observers:
                 observer.update()

     class ConcreteSubject(Subject):
         def some_business_logic(self):
             self.notify()

     class Observer:
         def update(self):
             pass

     class ConcreteObserver(Observer):
         def update(self):
             print("ConcreteObserver received an update")

     subject = ConcreteSubject()
     observer = ConcreteObserver()

     subject.attach(observer)
     subject.some_business_logic()
     ```

### 2. **Strategy Pattern**:
   - **Definition**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable. It allows the client to choose the appropriate algorithm at runtime.
   - **Real-World Analogy**: Choosing different navigation apps (e.g., Google Maps, Apple Maps) for driving directions.
   - **When to Use**: Use it when you want to define a family of interchangeable algorithms and make them easily switchable.
   - **Code Example**:
     ```python
     class Context:
         def __init__(self, strategy):
             self._strategy = strategy

         def do_operation(self):
             self._strategy.execute()

     class Strategy:
         def execute(self):
             pass

     class ConcreteStrategyA(Strategy):
         def execute(self):
             print("Executing strategy A")

     class ConcreteStrategyB(Strategy):
         def execute(self):
             print("Executing strategy B")

     context = Context(ConcreteStrategyA())
     context.do_operation()

     context._strategy = ConcreteStrategyB()
     context.do_operation()
     ```

### 3. **Command Pattern**:
   - **Definition**: Encapsulates a request as an object, thereby allowing for parameterization of clients with queues, requests, and operations.
   - **Real-World Analogy**: A remote control with buttons for various home appliances.
   - **When to Use**: Use it when you want to decouple sender and receiver of a request and allow for queuing or logging requests.
   - **Code Example**:
     ```python
     class Receiver:
         def perform_action(self):
             pass

     class Light(Receiver):
         def perform_action(self):
             print("Light is on")

     class TV(Receiver):
         def perform_action(self):
             print("TV is on")

     class Command:
         def __init__(self, receiver

):
             self._receiver = receiver

         def execute(self):
             pass

     class LightOnCommand(Command):
         def execute(self):
             self._receiver.perform_action()

     class TVOnCommand(Command):
         def execute(self):
             self._receiver.perform_action()

     class RemoteControl:
         def __init__(self):
             self._command = None

         def set_command(self, command):
             self._command = command

         def press_button(self):
             self._command.execute()

     light = Light()
     light_on_command = LightOnCommand(light)
     remote = RemoteControl()
     remote.set_command(light_on_command)
     remote.press_button()

     tv = TV()
     tv_on_command = TVOnCommand(tv)
     remote.set_command(tv_on_command)
     remote.press_button()
     ```

### 4. **State Pattern**:
   - **Definition**: Allows an object to alter its behavior when its internal state changes. The object will appear to change its class.
   - **Real-World Analogy**: A TV with different states (e.g., On, Off, Mute) that affect its behavior.
   - **When to Use**: Use it when an object's behavior changes based on its internal state, and it needs to switch between different behaviors dynamically.
   - **Code Example**:
     ```python
     class State:
         def handle(self):
             pass

     class TV:
         def __init__(self):
             self._state = None

         def set_state(self, state):
             self._state = state

         def press_button(self):
             self._state.handle()

     class OnState(State):
         def handle(self):
             print("TV is On")

     class OffState(State):
         def handle(self):
             print("TV is Off")

     class MuteState(State):
         def handle(self):
             print("TV is Muted")

     tv = TV()
     tv.set_state(OnState())
     tv.press_button()

     tv.set_state(OffState())
     tv.press_button()

     tv.set_state(MuteState())
     tv.press_button()
     ```

### 5. **Chain of Responsibility Pattern**:
   - **Definition**: Passes the request along a chain of handlers, each processing the request or passing it to the next handler in the chain.
   - **Real-World Analogy**: Customer support departments escalating issues to higher levels if they can't handle them.
   - **When to Use**: Use it when you want to avoid coupling the sender of a request to its receiver and allow multiple objects to handle the request.
   - **Code Example**:
     ```python
     class Handler:
         def set_next(self, handler):
             pass

         def handle_request(self, request):
             pass

     class ConcreteHandler(Handler):
         def __init__(self):
             self._next_handler = None

         def set_next(self, handler):
             self._next_handler = handler

         def handle_request(self, request):
             if request <= 10:
                 print(f"Handled request {request}")
             elif self._next_handler:
                 self._next_handler.handle_request(request)

     handler1 = ConcreteHandler()
     handler2 = ConcreteHandler()
     handler3 = ConcreteHandler()

     handler1.set_next(handler2)
     handler2.set_next(handler3)

     handler1.handle_request(5)
     handler1.handle_request(15)
     ```

### 6. **Interpreter Pattern**:
   - **Definition**: Provides a way to evaluate language grammar or expressions.
   - **Real-World Analogy**: A language interpreter that translates human language into machine instructions.
   - **When to Use**: Use it when you need to define a grammar for a simple language and provide a way to evaluate expressions in that language.
   - **Code Example** (simplified):
     ```python
     from abc import ABC, abstractmethod

     class AbstractExpression(ABC):
         @abstractmethod
         def interpret(self):
             pass

     class TerminalExpression(AbstractExpression):
         def __init__(self, data):
             self._data = data

         def interpret(self):
             return self._data

     class NonterminalExpression(AbstractExpression):
         def __init__(self, expression1, expression2):
             self._expression1 = expression1
             self._expression2 = expression2

         def interpret(self):
             return self._expression1.interpret() + self._expression2.interpret()

     expression1 = TerminalExpression(10)
     expression2 = TerminalExpression(20)
     expression3 = NonterminalExpression(expression1, expression2)
     result = expression3.interpret()
     ```

### 7. **Visitor Pattern**:
   - **Definition**: Represents an operation to be performed on elements of an object structure. It lets you define a new operation without changing the classes of the elements on which it operates.
   - **Real-World Analogy**: A tax auditor visiting different businesses to calculate their tax liabilities.
   - **When to Use**: Use it when you need to add new operations to existing classes without modifying those classes.
   - **Code Example**:
     ```python
     from abc import ABC, abstractmethod

     class Visitor(ABC):
         @abstractmethod
         def visit_element(self, element):
             pass

     class Element(ABC):
         @abstractmethod
         def accept(self, visitor):
             pass

     class ConcreteElementA(Element):
         def accept(self, visitor):
             visitor.visit_element(self)

         def operation_a(self):
             pass

     class ConcreteElementB(Element):
         def accept(self, visitor):
             visitor.visit_element(self)

         def operation_b(self):
             pass

     class ConcreteVisitorA(Visitor):
         def visit_element(self, element):
             if isinstance(element, ConcreteElementA):
                 element.operation_a()
             elif isinstance(element, ConcreteElementB):
                 element.operation_b()

     class ConcreteVisitorB(Visitor):
         def visit_element(self, element):
             if isinstance(element, ConcreteElementA):
                 element.operation_a()
             elif isinstance(element, ConcreteElementB):
                 element.operation_b()

     element_a = ConcreteElementA()
     element_b = ConcreteElementB()

     visitor_a = ConcreteVisitorA()
     visitor_b = ConcreteVisitorB()

     element_a.accept(visitor_a)
     element_b.accept(visitor_b)
     ```

### 8. **Memento Pattern**:
   - **Definition**: Captures and externalizes an object's internal state so the object can be restored to this state later.
   - **Real-World Analogy**: Saving and restoring checkpoints in a video game.
   - **When to Use**: Use it when you need to capture an object's state and be able to restore it to a previous state if needed.
   - **Code Example**:
     ```python
     class Memento:
         def __init__(self, state):
             self._state = state

         def get_state(self):
             return self._state

     class Originator:
         def __init__(self):
             self._state = ""

         def set_state(self, state):
             self._state = state

         def create_memento(self):
             return Memento(self._state)

         def restore_memento(self, memento):
             self._state = memento.get_state()

     class Caretaker:
         def __init__(self):
             self._mementos = []

         def add_memento(self, memento):
             self._mementos.append(memento)

         def get_memento(self

, index):
             return self._mementos[index]

     originator = Originator()
     caretaker = Caretaker()

     originator.set_state("State 1")
     memento1 = originator.create_memento()
     caretaker.add_memento(memento1)

     originator.set_state("State 2")
     memento2 = originator.create_memento()
     caretaker.add_memento(memento2)

     originator.restore_memento(caretaker.get_memento(0))
     print(originator._state)  # Output: State 1
     ```

These are some of the most common design patterns, along with their definitions, real-world analogies, use cases, and code examples. Keep in mind that design patterns are tools to help you solve common programming problems and improve code maintainability and flexibility. The choice of which pattern to use depends on the specific problem you're trying to solve and the context of your software project.
