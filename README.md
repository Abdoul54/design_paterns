# Design Patterns

## Creational Patterns:

### 1. **Singleton Pattern**:
   - **Real-world analogy**: The president's office, where there can only be one president at a time.
   - **Code Example** (Python):
     ```python
     class President:
         _instance = None

         def __new__(cls):
             if cls._instance is None:
                 cls._instance = super(President, cls).__new__(cls)
             return cls._instance

     president1 = President()
     president2 = President()

     print(president1 is president2)  # Output: True (they are the same instance)
     ```

### 2. **Factory Method Pattern**:
   - **Real-world analogy**: A car factory that produces cars of different models.
   - **Code Example** (Python):
     ```python
     from abc import ABC, abstractmethod

     class Car(ABC):
         @abstractmethod
         def drive(self):
             pass

     class Sedan(Car):
         def drive(self):
             return "Driving a sedan"

     class SUV(Car):
         def drive(self):
             return "Driving an SUV"

     def create_car(car_type):
         if car_type == "sedan":
             return Sedan()
         elif car_type == "suv":
             return SUV()

     car = create_car("suv")
     print(car.drive())  # Output: Driving an SUV
     ```

### 3. **Abstract Factory Pattern**:
   - **Real-world analogy**: A car manufacturer that produces both cars and their corresponding parts (e.g., engines, tires).
   - **Code Example** (Python):
     ```python
     from abc import ABC, abstractmethod

     class Car(ABC):
         @abstractmethod
         def drive(self):
             pass

     class Engine(ABC):
         @abstractmethod
         def start(self):
             pass

     class Sedan(Car):
         def drive(self):
             return "Driving a sedan"

     class SUV(Car):
         def drive(self):
             return "Driving an SUV"

     class ElectricEngine(Engine):
         def start(self):
             return "Starting an electric engine"

     class GasolineEngine(Engine):
         def start(self):
             return "Starting a gasoline engine"

     class CarFactory(ABC):
         @abstractmethod
         def create_car(self):
             pass

         @abstractmethod
         def create_engine(self):
             pass

     class SedanFactory(CarFactory):
         def create_car(self):
             return Sedan()

         def create_engine(self):
             return GasolineEngine()

     class SUVFactory(CarFactory):
         def create_car(self):
             return SUV()

         def create_engine(self):
             return ElectricEngine()

     factory = SedanFactory()
     car = factory.create_car()
     engine = factory.create_engine()
     print(car.drive())     # Output: Driving a sedan
     print(engine.start())  # Output: Starting a gasoline engine
     ```

### 4. **Builder Pattern**:
   - **Real-world analogy**: Building a custom meal at a restaurant by selecting various components (e.g., burger, fries, drink).
   - **Code Example** (Python):
     ```python
     class MealBuilder:
         def prepare_burger(self):
             pass

         def prepare_fries(self):
             pass

         def prepare_drink(self):
             pass

     class VegMealBuilder(MealBuilder):
         def prepare_burger(self):
             return "Veggie Burger"

         def prepare_fries(self):
             return "French Fries"

         def prepare_drink(self):
             return "Coke"

     class NonVegMealBuilder(MealBuilder):
         def prepare_burger(self):
             return "Chicken Burger"

         def prepare_fries(self):
             return "Chicken Fries"

         def prepare_drink(self):
             return "Pepsi"

     class MealDirector:
         def create_meal(self, builder):
             meal = {}
             meal["Burger"] = builder.prepare_burger()
             meal["Fries"] = builder.prepare_fries()
             meal["Drink"] = builder.prepare_drink()
             return meal

     veg_builder = VegMealBuilder()
     non_veg_builder = NonVegMealBuilder()
     director = MealDirector()

     veg_meal = director.create_meal(veg_builder)
     non_veg_meal = director.create_meal(non_veg_builder)

     print(veg_meal)
     print(non_veg_meal)
     ```

### 5. **Prototype Pattern**:
   - **Real-world analogy**: Making photocopies of a master document.
   - **Code Example** (Python):
     ```python
     import copy

     class Prototype:
         def clone(self):
             pass

     class ConcretePrototype(Prototype):
         def __init__(self, value):
             self._value = value

         def clone(self):
             return copy.deepcopy(self)

     prototype = ConcretePrototype("Initial Value")
     copy1 = prototype.clone()
     copy2 = prototype.clone()

     print(copy1._value)  # Output: Initial Value
     print(copy2._value)  # Output: Initial Value

     copy1._value = "Modified Value"
     print(prototype._value)  # Output: Initial Value
     print(copy1._value)     # Output: Modified Value
     ```

## Structural Patterns:

### 1. **Adapter Pattern**:
   - **Real-world analogy**: Using an adapter to connect a European plug to a US socket.
   - **Code Example** (Python):
     ```python
     class EuropeanPlug:
         def plug_in_european_socket(self):
             print("Plugged into European socket")

     class USAdapter:
         def __init__(self, european_plug):
             self._european_plug = european_plug

         def plug_in_us_socket(self):
             print("Plugged into US socket")
             self._european_plug.plug_in_european_socket()

     european_plug = EuropeanPlug()
     adapter = USAdapter(european_plug)
     adapter.plug_in_us_socket()

     # Output:
     # Plugged into US socket
     # Plugged into European socket
     ```

### 2. **Bridge Pattern**:
   - **Real-world analogy**: Building a TV remote control that can work with different TV models.
   - **Code Example** (Python):
     ```python
     from abc import ABC, abstractmethod

     class Device(ABC):
         @abstractmethod
         def turn_on(self):
             pass

         @abstractmethod
         def turn_off(self):
             pass

     class TV(Device):
         def turn_on(self):
             print("TV is ON")

         def turn_off(self):
             print("TV is OFF")

     class RemoteControl:
         def __init__(self, device):
             self._device = device

         def turn_on(self):
             self._device.turn_on()

         def turn_off(self):
             self._device.turn_off()

     tv = TV()
     remote = RemoteControl(tv)

     remote.turn_on()  # Output: TV is ON
     remote.turn_off() # Output: TV is OFF
     ```

### 3. **Composite Pattern**:
   - **Real-world analogy**: A company organization structure, with departments containing employees and sub-departments.


   - **Code Example** (Python):
     ```python
     class Employee:
         def __init__(self, name):
             self._name = name

         def display(self):
             print(self._name)

     class Department:
         def __init__(self, name):
             self._name = name
             self._employees = []

         def add_employee(self, employee):
             self._employees.append(employee)

         def display(self):
             print(self._name)
             for employee in self._employees:
                 employee.display()

     employee1 = Employee("Alice")
     employee2 = Employee("Bob")
     employee3 = Employee("Charlie")

     department1 = Department("HR")
     department1.add_employee(employee1)
     department1.add_employee(employee2)

     department2 = Department("Engineering")
     department2.add_employee(employee3)

     company = Department("Company")
     company.add_employee(department1)
     company.add_employee(department2)

     company.display()
     ```

### 4. **Decorator Pattern**:
   - **Real-world analogy**: Adding toppings to a pizza.
   - **Code Example** (Python):
     ```python
     class Pizza:
         def cost(self):
             return 10

     class TomatoTopping:
         def __init__(self, pizza):
             self._pizza = pizza

         def cost(self):
             return self._pizza.cost() + 2

     class CheeseTopping:
         def __init__(self, pizza):
             self._pizza = pizza

         def cost(self):
             return self._pizza.cost() + 3

     pizza = Pizza()
     pizza_with_toppings = CheeseTopping(TomatoTopping(pizza))
     print(pizza_with_toppings.cost())  # Output: 15
     ```

### 5. **Facade Pattern**:
   - **Real-world analogy**: Using a remote control to operate a complex home theater system.
   - **Code Example** (Python):
     ```python
     class Amplifier:
         def turn_on(self):
             print("Amplifier is ON")

         def turn_off(self):
             print("Amplifier is OFF")

     class DVDPlayer:
         def turn_on(self):
             print("DVD Player is ON")

         def turn_off(self):
             print("DVD Player is OFF")

     class HomeTheaterFacade:
         def __init__(self, amplifier, dvd_player):
             self._amplifier = amplifier
             self._dvd_player = dvd_player

         def watch_movie(self):
             self._amplifier.turn_on()
             self._dvd_player.turn_on()
             print("Movie is playing")

         def end_movie(self):
             self._dvd_player.turn_off()
             self._amplifier.turn_off()
             print("Movie has ended")

     amplifier = Amplifier()
     dvd_player = DVDPlayer()
     theater = HomeTheaterFacade(amplifier, dvd_player)

     theater.watch_movie()  # Output: Amplifier is ON, DVD Player is ON, Movie is playing
     theater.end_movie()    # Output: DVD Player is OFF, Amplifier is OFF, Movie has ended
     ```

### 6. **Flyweight Pattern**:
   - **Real-world analogy**: Using a shared bike service, where many users share the same bikes.
   - **Code Example** (Python):
     ```python
     class Bike:
         def __init__(self, bike_type):
             self._bike_type = bike_type

         def ride(self, user):
             print(f"{user} is riding a {self._bike_type} bike")

     class BikeFactory:
         _bikes = {}

         @staticmethod
         def get_bike(bike_type):
             if bike_type not in BikeFactory._bikes:
                 BikeFactory._bikes[bike_type] = Bike(bike_type)
             return BikeFactory._bikes[bike_type]

     users = ["User A", "User B", "User C"]

     for user in users:
         bike = BikeFactory.get_bike("Mountain")
         bike.ride(user)

     # Output:
     # User A is riding a Mountain bike
     # User B is riding a Mountain bike
     # User C is riding a Mountain bike
     ```

## Behavioral Patterns:

### 1. **Observer Pattern**:
   - **Real-world analogy**: Subscribing to a YouTube channel to get notified of new videos.
   - **Code Example** (Python):
     ```python
     class YouTuber:
         def __init__(self):
             self.subscribers = []

         def subscribe(self, subscriber):
             self.subscribers.append(subscriber)

         def upload_video(self, video):
             print("New video uploaded!")
             for subscriber in self.subscribers:
                 subscriber.notify(video)

     class Subscriber:
         def notify(self, video):
             print(f"Received a notification: New video - {video}")

     youtuber = YouTuber()
     subscriber1 = Subscriber()
     subscriber2 = Subscriber()

     youtuber.subscribe(subscriber1)
     youtuber.subscribe(subscriber2)
     youtuber.upload_video("How to Code")

     # Output:
     # New video uploaded!
     # Received a notification: New video - How to Code
     # Received a notification: New video - How to Code
     ```

### 2. **Strategy Pattern**:
   - **Real-world analogy**: Choosing different characters in a video game, each with unique abilities.
   - **Code Example** (Python):
     ```python
     class Character:
         def __init__(self, strategy):
             self.strategy = strategy

         def attack(self):
             self.strategy.attack()

     class SwordAttack:
         def attack(self):
             print("Attacking with a sword!")

     class BowAttack:
         def attack(self):
             print("Attacking with a bow!")

     character1 = Character(SwordAttack())
     character2 = Character(BowAttack())

     character1.attack()  # Output: Attacking with a sword!
     character2.attack()  # Output: Attacking with a bow!
     ```

### 3. **Command Pattern**:
   - **Real-world analogy**: Remote control with buttons to perform actions like turning on/off a TV.
   - **Code Example** (Python):
     ```python
     from abc import ABC, abstractmethod

     class Command(ABC):
         @abstractmethod
         def execute(self):
             pass

     class Light:
         def turn_on(self):
             print("Light is ON")

         def turn_off(self):
             print("Light is OFF")

     class LightOnCommand(Command):
         def __init__(self, light):
             self._light = light

         def execute(self):
             self._light.turn_on()

     class LightOffCommand(Command):
         def __init__(self, light):
             self._light = light

         def execute(self):
             self._light.turn_off()

     class RemoteControl:
         def __init__(self):
             self._command = None

         def set_command(self, command):
             self._command = command

         def press_button(self):
             self._command.execute()

     light = Light()
     light_on = LightOnCommand(light)
     light_off = LightOffCommand(light)

     remote = RemoteControl()
     remote.set_command(light_on)
     remote.press_button()  # Output: Light is ON
     remote.set_command(light_off)
     remote.press_button()  # Output:

 Light is OFF
     ```

### 4. **State Pattern**:
   - **Real-world analogy**: A TV can be in different states like ON, OFF, or MUTE, and you can switch between these states.
   - **Code Example** (Python):
     ```python
     class TVState(ABC):
         @abstractmethod
         def handle(self):
             pass

     class TV:
         def __init__(self):
             self._state = None

         def set_state(self, state):
             self._state = state

         def press_button(self):
             self._state.handle()

     class TVOn(TVState):
         def handle(self):
             print("TV is ON")

     class TVOff(TVState):
         def handle(self):
             print("TV is OFF")

     class TVMute(TVState):
         def handle(self):
             print("TV is MUTE")

     tv = TV()
     tv.set_state(TVOn())
     tv.press_button()  # Output: TV is ON
     tv.set_state(TVOff())
     tv.press_button()  # Output: TV is OFF
     tv.set_state(TVMute())
     tv.press_button()  # Output: TV is MUTE
     ```

### 5. **Chain of Responsibility Pattern**:
   - **Real-world analogy**: Passing a request through a chain of managers in an organization until one of them approves it.
   - **Code Example** (Python):
     ```python
     class Manager:
         def __init__(self, name):
             self._name = name
             self._successor = None

         def set_successor(self, successor):
             self._successor = successor

         def handle_request(self, request):
             pass

     class TeamLead(Manager):
         def handle_request(self, request):
             if request <= 2:
                 print(f"Team Lead {self._name} approved the request.")
             elif self._successor is not None:
                 self._successor.handle_request(request)

     class ProjectManager(Manager):
         def handle_request(self, request):
             if request <= 5:
                 print(f"Project Manager {self._name} approved the request.")
             elif self._successor is not None:
                 self._successor.handle_request(request)

     class Director(Manager):
         def handle_request(self, request):
             if request <= 10:
                 print(f"Director {self._name} approved the request.")
             else:
                 print(f"Director {self._name} cannot approve the request.")

     team_lead = TeamLead("Alice")
     project_manager = ProjectManager("Bob")
     director = Director("Charlie")

     team_lead.set_successor(project_manager)
     project_manager.set_successor(director)

     team_lead.handle_request(3)  # Output: Team Lead Alice approved the request.
     team_lead.handle_request(7)  # Output: Director Charlie cannot approve the request.
     ```

### 6. **Interpreter Pattern**:
   - **Real-world analogy**: A language translator that interprets spoken words from one language to another.
   - **Code Example** (Python):
     ```python
     from abc import ABC, abstractmethod

     class Expression(ABC):
         @abstractmethod
         def interpret(self, context):
             pass

     class NumberExpression(Expression):
         def __init__(self, number):
             self._number = number

         def interpret(self, context):
             return self._number

     class AddExpression(Expression):
         def __init__(self, left, right):
             self._left = left
             self._right = right

         def interpret(self, context):
             return self._left.interpret(context) + self._right.interpret(context)

     class Context:
         def __init__(self):
             self._variables = {}

         def set_variable(self, variable, value):
             self._variables[variable] = value

         def get_variable(self, variable):
             return self._variables.get(variable, 0)

     context = Context()
     context.set_variable("x", 5)
     context.set_variable("y", 10)

     expression = AddExpression(NumberExpression(context.get_variable("x")), NumberExpression(context.get_variable("y")))
     result = expression.interpret(context)
     print(f"Result: {result}")  # Output: Result: 15
     ```

### 7. **Visitor Pattern**:
   - **Real-world analogy**: A tour guide who takes visitors through different places and provides information at each location.
   - **Code Example** (Python):
     ```python
     from abc import ABC, abstractmethod

     class Visitor(ABC):
         @abstractmethod
         def visit(self, element):
             pass

     class Element(ABC):
         @abstractmethod
         def accept(self, visitor):
             pass

     class Museum(Element):
         def accept(self, visitor):
             visitor.visit(self)

     class Zoo(Element):
         def accept(self, visitor):
             visitor.visit(self)

     class VisitorImpl(Visitor):
         def visit(self, element):
             if isinstance(element, Museum):
                 print("Visited the Museum")
             elif isinstance(element, Zoo):
                 print("Visited the Zoo")

     elements = [Museum(), Zoo()]
     visitor = VisitorImpl()

     for element in elements:
         element.accept(visitor)

     # Output:
     # Visited the Museum
     # Visited the Zoo
     ```

### 8. **Memento Pattern**:
   - **Real-world analogy**: Saving game progress at checkpoints and being able to restore the game to a previous state.
   - **Code Example** (Python):
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

         def get_state(self):
             return self._state

         def create_memento(self):
             return Memento(self._state)

         def restore_state(self, memento):
             self._state = memento.get_state()

     class Caretaker:
         def __init__(self):
             self._mementos = []

         def add_memento(self, memento):
             self._mementos.append(memento)

         def get_memento(self, index):
             return self._mementos[index]

     originator = Originator()
     caretaker = Caretaker()

     originator.set_state("State 1")
     caretaker.add_memento(originator.create_memento())

     originator.set_state("State 2")
     caretaker.add_memento(originator.create_memento())

     originator.restore_state(caretaker.get_memento(0))
     print(originator.get_state())  # Output: State 1
     ```

These examples should give you a deeper understanding of various design patterns, their real-world analogies, and how they can be implemented in Python to solve specific software design problems. Design patterns help make your code more organized, maintainable, and flexible.
