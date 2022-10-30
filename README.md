# Patterns
Codification from patterns of Advanced Python II


#------------------------------------------------Patrones Arquitectonicos de Diseño de Software-----------------------------------------------------------------------

Son técnicas o métodos para resolver problemas comunes orientados hacia el diseño de interacción o interfaces, es decir una solución a un 
problema con el diseño. En considerar a un solución como patron es necesario que el mismo contenga ciertas características:
        #Debe comprobar la efectividad dando resolución a problematicas similares previas.
        #Debe ser reutilizable, aplicable a diversidades circunsatanciales en cuanto a problemas de diseño se refiere.

#-Objetivos:

Estos pretenden :
    # Proporcionar catálogos de elementos reusables en el diseño de sistemas de software.
    # Evitar la reiteración en la busqueda de soluciones a problemas ya conocidos y solucionados previamente.
    # Formalizar un vocabulario común entre diseñadores

#-Categorías:

Por escala o nivel de abstracción:
    #Patron de arquitectura: Expresa un equema organizado estructural fundamental para sitemas de software.
    #Patrones de diseño: Aquellos que expresan esquemas para deginir estructuras de diseño (o sus relaciones)
    #con las que construir sistemas de software.
    #Dialectos : Patrones de nivel bajo especificos para un lenguaje de programación o entorno concreto.

#Antipatrones:
 
Se reduce en dar a conocer los problemas que acarrean ciertos diseños muy frecuentes, para intentar evitar que diferentes 
sistemas acaben una y otra vez en el mismo callejón sin salida por haber cometido los mismos errores. 
 

#Los patrones se dividen en varios tipos como:
 
    #Singleton
    -Fábrica (Factory)
    -Fábrica abstracta (Abstract factory)
    -Prototipo (Prototype)
    -Fachada (Facade)
    -Decorador (Decorator)
    -Proxy
    -Command
    -Memento
    -Observador (Observer)
    -Estrategia (Strategy)
    -DAO (Data Access Object)
    -Inyección de dependencias (Dependency injection)
    -MVC Modelo Vista Controlador (Model View Controller)     

----------------Singleton--------------------------------

Patron de diseño creacional que permite asegurar que una clase tenga una unica instancia, a la vez que proporciona un punto de
acceso global a dicha distancia; Esto se puede definir como un conjunto que posee solamente un elemento.

EJEMPLO:

class SoyUnico(object):

    __instance = None
    nombre = None

    def __str__(self):
        return 'self' + ' ' + self.nombre

    def __new__(cls):
        if SoyUnico.__instance is None:
            SoyUnico.__instance = object.__new__(cls)
        return SoyUnico.__instance

ricardo = SoyUnico()
ricardo.nombre = "Ricardo Moya"
print(ricardo)
ramon = SoyUnico()
ramon.nombre = "Ramón Invarato"
print(ramon)

print(ricardo)
print(ramon)


----------------Factory--------------------------------

Define a una interfaz para la creación de un objeto, optando a que las subclases tomen decisión en que clase instanciar, esto 
permite que una clase difiera la creación de instancias a las subclases; define constructores virtuales, los cuales asignan 
valores a los elementos de clase cuando se crea un objeto de esa misma clase.


EJEMPLO

from __future__ import annotations
from abc import ABC, abstractmethod
from cmath import sin
from tkinter import E


class Creator(ABC):
    
    @abstractmethod
    def factory_method(self):      
        pass
    def some_operation(self) -> str:     
        # Call the factory method to create a Product object.
        product = self.factory_method()
        # Now, use the product.
        result = f"Creator: The same creator's code has just worked with {product.operation()}"
        return result

class ConcreteCreator1(Creator):   
    def factory_method(self) -> Product:
        return ConcreteCreator1()

class ConcreteCreator2(Creator):
    def factory_method(self) -> Product:
        return ConcreteCreator2()


----------------Abstract Factory--------------------------------

Aporta una interfaz que crea familias de objetos en relación entre si o independientes sin especificar sus clases concretas,
permite una jerarquía que ecierra muchas plataformas posibles y construcción de un conjunto de productos. Es un metodo de 
fabrica por producto, y su principal próposito es proporcionar una interfaz para crear familias de objetos relacionados, sin
especificar clases concretas. Puede almacenar un conjunto de prototipos a partir de los cuales clonar y devolver objetos de 
productos.

EJEMPLO

import abc
class AbstractFactory(metaclass=abc.ABCMeta):
    """
    Declare an interface for operations that create abstract product
    objects.
    """
    @abc.abstractmethod
    def create_product_a(self):
        pass

    @abc.abstractmethod
    def create_product_b(self):
        pass

class ConcreteFactory1(AbstractFactory):
    """
    Implement the operations to create concrete product objects.
    """
    def create_product_a(self):
        return ConcreteProductA1()

    def create_product_b(self):
        return ConcreteProductB1()

class ConcreteFactory2(AbstractFactory):
    """
    Implement the operations to create concrete product objects.
    """
    def create_product_a(self):
        return ConcreteProductA2()

    def create_product_b(self):
        return ConcreteProductB2()

class AbstractProductA(metaclass=abc.ABCMeta):
    """
    Declare an interface for a type of product object.
    """
    @abc.abstractmethod
    def interface_a(self):
        pass
class ConcreteProductA1(AbstractProductA):
    """
    Define a product object to be created by the corresponding concrete
    factory.
    Implement the AbstractProduct interface.
    """
    def interface_a(self):
        pass
class ConcreteProductA2(AbstractProductA):
    """
    Define a product object to be created by the corresponding concrete
    factory.
    Implement the AbstractProduct interface.
    """
    def interface_a(self):
        pass
class AbstractProductB(metaclass=abc.ABCMeta):
    """
    Declare an interface for a type of product object.
    """
    @abc.abstractmethod
    def interface_b(self):
        pass
class ConcreteProductB1(AbstractProductB):
    """
    Define a product object to be created by the corresponding concrete
    factory.
    Implement the AbstractProduct interface.
    """
    def interface_b(self):
        pass
class ConcreteProductB2(AbstractProductB):
    """
    Define a product object to be created by the corresponding concrete
    factory.
    Implement the AbstractProduct interface.
    """
    def interface_b(self):
        pass
def main():
    for factory in (ConcreteFactory1(), ConcreteFactory2()):
        product_a = factory.create_product_a()
        product_b = factory.create_product_b()
        product_a.interface_a()
        product_b.interface_b()
if __name__ == "__main__":
    main()


----------------Prototype--------------------------------

Patrón de diseño creacional que permite copiar objetos existentes sin que el código dependa de sus clases,
este delega el proceso de clonación a los propios objetos que estan siendo clonados >> declara la interfaz
común para todos los objetos que soporten clonación pues, nos permite clonar un objeto sin acoplar el có-
digo a la clase de ese objeto. Normalmente, aquella interfaz contiene un único método ("clone")


EJEMPLO

import copy

class Prototype:
    pass

def main():
    Dataprototype = Prototype()
    Dataprototype_copy = copy.deepcopy(Dataprototype)

if __name__ == "__main__":
    main()

----------------Facade(fachada)--------------------------------

Es un patrón el cual proporciona una interfaz simplificada a una bliblioteca, un framework o cualquier
otro grupo complejo de clases. Encasillando este concepto a la vida real; puede referenciarse a la per-
fección con el pedido que se hace por medio del telefono, el operador es la fachada a todos los servi-
cios y departamentos de la tienda. El operador proporciona una simple interfaz de voz al sistema de pe-
didos, pasarselas de pago y varios servicios de entrega


EJEMPLO

class Facade:
    """
    Know which subsystem classes are responsible for a request.
    Delegate client requests to appropriate subsystem objects.
    """
    def __init__(self):
        self._subsystem_1 = Subsystem1()
        self._subsystem_2 = Subsystem2()
    def operation(self):
        self._subsystem_1.operation1()
        self._subsystem_1.operation2()
        self._subsystem_2.operation1()
        self._subsystem_2.operation2()
class Subsystem1:
    """
    Implement subsystem functionality.
    Handle work assigned by the Facade object.
    Have no knowledge of the facade; that is, they keep no references to
    it.
    """
    def operation1(self):
        pass
    def operation2(self):
        pass
class Subsystem2:
    """
    Implement subsystem functionality.
    Handle work assigned by the Facade object.
    Have no knowledge of the facade; that is, they keep no references to
    it.
    """
    def operation1(self):
        pass
    def operation2(self):
        pass
def main():
    facade = Facade()
    facade.operation()
if __name__ == "__main__":
    main()

----------------Decorator--------------------------------

Patron de diseño de tipo estructural que permite añadir funcionalidades a objetos colocando estos obje-
tos dentro de objetos encapsulandores especiales que contienen estas funcionalidades. Adiciona responsa-
bilidades adicionales a un objeto de forma dinámica. En el ambiente real vestir ropa es perfecto ejemplar
de uso de decoradores, cuando hace frío uno se cubre con un suéter, y si el frío en el cuerpo persiste es
posible incrementar la tempertatura con otro abrigo, además, si esta lloviendo se puede colocar un 
impermeable; básicamente todas estas prendas extienden el comportamiento básico pero no son parte de uno 
mismo y es posible retirar cualquiera de las prendas cuando el sujeto lo prefiera.


EJEMPLO

"""
Attach additional responsibilities to an object dynamically. Decorators
provide a flexible alternative to subclassing for extending
functionality.
"""

import abc

class Component(metaclass=abc.ABCMeta):
    """
    Define the interface for objects that can have responsibilities
    added to them dynamically.
    """
    @abc.abstractmethod
    def operation(self):
        pass
class Decorator(Component, metaclass=abc.ABCMeta):
    """
    Maintain a reference to a Component object and define an interface
    that conforms to Component's interface.
    """
    def __init__(self, component):
        self._component = component
    @abc.abstractmethod
    def operation(self):
        pass

class ConcreteDecoratorA(Decorator):
    """
    Add responsibilities to the component.
    """
    def operation(self):
        # ...
        self._component.operation()
        # ...
class ConcreteDecoratorB(Decorator):
    """
    Add responsibilities to the component.
    """
    def operation(self):
        # ...
        self._component.operation()
        # ...
class ConcreteComponent(Component):
    """
    Define an object to which additional responsibilities can be
    attached.
    """
    def operation(self):
        pass
def main():
    concrete_component = ConcreteComponent()
    concrete_decorator_a = ConcreteDecoratorA(concrete_component)
    concrete_decorator_b = ConcreteDecoratorB(concrete_decorator_a)
    concrete_decorator_b.operation()
if __name__ == "__main__":
    main()


----------------Proxy--------------------------------

Patron de diseño de clase estructural que permite proporcionar un sustituto o marcador de posición para
otro objeto. Un proxy controla el acceso al objeto original, permitiendo hacer algo antes o despues de 
que la solicitud llegue al objeto original. Una tarjeta de crédito es un proxy de una cuenta bancaria, 
que, a su vez, es un proxy de un manojo de billetes. Ambos implementan la misma interfaz, por lo que 
pueden utilizarse para realizar un pago. El consumidor se siente genial porque no necesita llevar un 
montón de efectivo encima. El dueño de la tienda también está contento porque los ingresos de la transa
cción se añaden electrónicamente a la cuenta bancaria de la tienda sin el riesgo de perder el depósito o
sufrir un robo de camino al banco.


EJEMPLO


import abc

class Subject(metaclass=abc.ABCMeta):
    
    @abc.abstractmethod
    def request(self):
        pass

class Proxy(Subject):
   
    def __init__(self, real_subject):
        self._real_subject = real_subject
    def request(self):
        # ...
        self._real_subject.request()
        # ...
class RealSubject(Subject):
   
    def request(self):
        pass

def main():
    real_subject = RealSubject()
    proxy = Proxy(real_subject)
    proxy.request()

if __name__ == "__main__":
    main()

----------------Command--------------------------------

Patron de diseño de comportamiento que convierte a una solicitud en un objeto indepentiente que contiene
toda la información sobre la solicitud. Permite parametrizar los métodos con diferentes solicitudes,
retrasar o poner en cola la ejecución de una solicitud y soportar operciones que no se pueden realizar.
Como aproximado en la vida real, un sujeto entra a un restaurante y se sienta en una mesa junto a la 
ventana. El camarero se acerca y toma el pedido a la pared. Al cabo de un rato, el pedido llega al chef,
que lo lee y prepara la comida. el cocinero coloca la comida en una bandeja junto al pedido. El camarero
descubre la bandeja, comprueba el pedido para asegurarse de que todo está como lo solicito el sujeto, y 
luego lo lleva a la mesa. El pedido en papel hace la función de un comando. Permanece en una cola hasta 
que el chef está listo para servirlo. Este pedido contiene toda la información relevante necesaria para 
preparar la comida. Permite al chef empezar a cocinar de inmediato, en lugar de tener que correr de un 
lado a otro aclarando los detalles del pedido directamente


EJEMPLO

import abc

class Invoker:
    """
    Ask the command to carry out the request.
    """
    def __init__(self):
        self._commands = []

    def store_command(self, command):
        self._commands.append(command)

    def execute_commands(self):
        for command in self._commands:
            command.execute()

class Command(metaclass=abc.ABCMeta):
    """
    Declare an interface for executing an operation.
    """
    def __init__(self, receiver):
        self._receiver = receiver
    @abc.abstractmethod
    def execute(self):
        pass
class ConcreteCommand(Command):
    """
    Define a binding between a Receiver object and an action.
    Implement Execute by invoking the corresponding operation(s) on
    Receiver.
    """
    def execute(self):
        self._receiver.action()

class Receiver:
    """
    Know how to perform the operations associated with carrying out a
    request. Any class may serve as a Receiver.
    """
    def action(self):
        pass
def main():
    receiver = Receiver()
    concrete_command = ConcreteCommand(receiver)
    invoker = Invoker()
    invoker.store_command(concrete_command)
    invoker.execute_commands()

if __name__ == "__main__":
    main()

    
----------------Memento--------------------------------

Patron de diseño de comportamiento que permite guardar y restaurar el estado previo de un objeto sin reve
lar los detalles de su implementación 

import pickle

class Originator:
    """
    Create a memento containing a snapshot of its current internal
    state.
    Use the memento to restore its internal state.
    """
    def __init__(self):
        self._state = None
    def set_memento(self, memento):
        previous_state = pickle.loads(memento)
        vars(self).clear()
        vars(self).update(previous_state)
    def create_memento(self):
        return pickle.dumps(vars(self))

def main():
    originator = Originator()
    memento = originator.create_memento()
    originator._state = True
    originator.set_memento(memento)

if __name__ == "__main__":
    main()


----------------Observer--------------------------------

Patrón de diseño de comportamiento que permite la definición de un mecanismo de suscripción para notificar
a varios objetos sobre cualquier evento que le suceda al objeto que estan observando


EJEMPLO

import abc

class Subject:
    def __init__(self):
        self._observers = set()
        self._subject_state = None
    def attach(self, observer):
        observer._subject = self
        self._observers.add(observer)
    def detach(self, observer):
        observer._subject = None
        self._observers.discard(observer)
    def _notify(self):
        for observer in self._observers:
            observer.update(self._subject_state)
    @property
    def subject_state(self):
        return self._subject_state
    @subject_state.setter
    def subject_state(self, arg):
        self._subject_state = arg
        self._notify()

class Observer(metaclass=abc.ABCMeta):
    def __init__(self):
        self._subject = None
        self._observer_state = None
    @abc.abstractmethod
    def update(self, arg):
        pass
class ConcreteObserver(Observer):
    def update(self, arg):
        self._observer_state = arg
        # ...
def main():
    subject = Subject()
    concrete_observer = ConcreteObserver()
    subject.attach(concrete_observer)
    subject.subject_state = 123

if __name__ == "__main__":
    main()

----------------Strategy--------------------------------

Patrón de diseño de comportamiento que permite difinir una familia de algoritmos, colocar cada uno en una 
clase separada y hacer sus objetos intercambiables. Esto permite que tome aquella clase que hace algo espe
cífico de varias maneras distintas y se extraigan todos los algoritmos para colocarlos en clases separadas,
a las cuales se les nombra como strategy. Una situación aplicado a la vida real  es cuando se tiene que 
llegar al aeropuerto, se pude tomar el autobús, pedir un taxi o ir en bicicleta. Son estrategias posibles de
transporte, se pueden elegir alguna de las estrategias presentadas, dependiendo de factores como el
presupuesto o los límites de tiempo. 


EJEMPLO

import abc

class Context:
    def __init__(self, strategy):
        self._strategy = strategy
    def context_interface(self):
        self._strategy.algorithm_interface()
class Strategy(metaclass=abc.ABCMeta):
    @abc.abstractmethod
    def algorithm_interface(self):
        pass
class ConcreteStrategyA(Strategy):
    def algorithm_interface(self):
        pass
class ConcreteStrategyB(Strategy):
    def algorithm_interface(self):
        pass
def main():
    concrete_strategy_a = ConcreteStrategyA()
    context = Context(concrete_strategy_a)
    context.context_interface()

if __name__ == "__main__":
    main()


----------------DAO(Data Access Object)--------------------------------

Patrón arquitectonico que permite separar la lógica de acceso a datos de los Bussines Objects u Objetos 
de negocios, de tal forma que el DAO encapsula toda la lógica de acceso de datos al resto de la 
aplicación. Hace una fácil implementación y proporciona claros beneficios si se tiene una fuente de datos
y no cambia, ya que permite separar por completo la lógica de acceso a datos en una capa separada y, de  
esta manera solo se es necesario preocuparse por la misma lógica de negocio sin tener importancia la
procedencia de los datos o los detalles de los técnicos para consultarlos para consultarlos o 
actualizarlos.


----------------Dependency Injection--------------------------------

Es todo lo que una clase necesita para poder funcionar. Para este ejemplo la clase Computadora necesita de
la clase Monitor para poder crear una nueva instancia de ella, es decir la clase Computadora depende del la
clase Monitor, y su vez la clase Monitor es una dependencia de la clase Computadora. Un objeto de tipo 
Computadora no puede ser creado sin antes haberse creado un objeto de tipo Monitor. Es posible desacoplar los
componentes de la aplicación de manera mas sencilla, delegando responsabilidades únicas a diferentes piezas de 
software, lo cual a su vez permitirá tener código mucho más flexible, fácil testeo, fácil lectura y por 
encima de todo fácil de mantener.


EJEMPLO

class Monitor:
    pass

class Computadora:
    def __init__(self):
       self.monitor= Monitor() # <-- dependency

----------------MVC Modelo Vista Controlador (Model View Controller)--------------------------------

Patrón arquitectural es decir que nos dicta una arquitectura como modelo o guía para el desarrollo de aplica
ciones. Dicta como se estructura cada uno de los componentes del software, las responsabilidades de cada uno
y las relaciones entre ellos, dicta como dividir el software en componentes según la finalidad de cada 
uno estructurando el código de manera funcional y modular.Funcional porque cada bloque de código se ubicará 
dentro del componente según su función o rol. 
