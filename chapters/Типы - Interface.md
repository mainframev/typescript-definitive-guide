# Типы — Interfaces
________________

Несмотря на то, что тема относящаяся к интерфесам очень проста, именно она вызывает наибольшее количество вопросов у начинающих разработчиков. Поэтому такие вопросы как для чего нужны интерфейсы, когда их применять, а когда нет, будет подробно рассмотренны в этой главе.


## Общая теория

По факту интерфейс затрагивает сразу несколько аспектов создания программ относящихся к проектированию, реализации, конечной сборке. Поэтому чтобы понять предназначение интерфейса необходимо рассмотреть каждый аспект по отдельности.

Первый аспект (реализация) предлагает рассматривать создаваемые экземпляры как социальные объекты чья публичная часть инфраструктуры была оговорена в контракте, к коему относится интерфейс. Другими словами интерфейс это контракт реализация которого гарантирует наличие оговоренных в нем членов потребителю экземпляра. Поскольку интерфейс описывает исключительно типы членов объекта (поля, свойства, сигнатуры методов) они не могут гарантировать что сопряженная с ними логика будет соответствовать каким-либо критериям. Поэтому случаю была принята методология называемая _контрактное программирование_. Несмотря на то что данная методология вызывает непонимание у большинства начинающих разработчиков, в действительности она очень проста. За этим таинственным термином скрываются рекомендации придерживатся устной или писменной спецификации при реализации логики сопряженной с оговоренными в интерфейсе членами.

Второй аспект (проектирование) предлагает проектировать объекты менее независимыми за счет отказа от конкретных типов (классов) в пользу интерфейсов. Ведь пока тип переменной или параметра представляется классовым типом, невозможно будет присвоить значение соответствующее, но не совместимое с ним. Под соответствующим имеется ввиду соответствующим по всем признакам, но не состоящим в отношениях наследовния. И хотя в _TypeScript_ из-за реализации _номинативной типизации_ подобной проблемы не существует, по возможности рекомендуется придерживатся классических взглядов.

Третий аспект (сборка) вытекает из второго и предполагает уменьшение размера компилируемого пакета (_bandle_) за счет отказа от конкретных типов (классов). Фактически если какой-либо объект требуется пакету лишь для выполнения операций над ним, последнему вовсе не нужно содержать определение первого. Другими словами скомпелированный пакет не должен включать определение класса со всей его логикой только потому, что он указан в качестве типа. Для этого как нельзя лучше подходят типы представленные интерфейсами. Хотя нельзя не упомянуть о том, что данная проблема не имеет никакого практического отношения к разработчикам на языке _TypeScript_ поскольку его (или точнее сказать _JavaScript_) модульная система лишена подобного недостатка.

Вот эти несколько строк описывающие оговоренные в самом начале аспекты заключают в себе ответы на все возможные вопросы которые только могут возникнуть относительно темы сопряженной с интерфейсами. Если ещё более доступно, то интерфейсы нужны для снижения зависимости и наложения обязательств на реализующие их классы. Кроме того интерфейсы стоит применять всегда и везде где только можно. Это не только повысит семантическую привлекательность кода, но и сделает его более поддерживаемым.

Не лишним будет добавить что интерфейсы являются фундаментальной составляющей идеологии как типизированных языков, так и объектно-ориентированного программирования.

Такая известная группа программистов, как _“Банда четырех”_ (_Gang of Four_, сокращённо _GoF_), в своей книге, положившей начало популяризации шаблонов проектирования, описывали интерфейс как ключевую концепцию _объектно-ориентированного программирования_ (_ооп_). Понятие интерфейса является настолько важным, что в книге был сформулирован принцип объектно-ориентированного проектирования, который звучит так: _Программируйте в соответствии с интерфейсом, а не с реализацией._

Другими словами, авторы советуют создавать систему, которой вообще ничего не будет известно о реализации. Проще говоря, создаваемая система должна быть построена на типах, определяемых интерфейсами, а не на типах, определяемых классами.

С теорией закончено. Осталось подробно рассмотреть реализацию интерфейсов в _TypeScript_.


## Интерфейс в TypeScript

_TypeScript_ предлагает новый тип данных, определяемый с помощью синтаксической конструкции называемой _интерфейс_ (`interface`). 

`Interface` — это синтаксическая конструкция предназначенная для описания открытой (`public`) части объекта без реализации. Хотя не будет лишним упомянуть, что существуют языки позволяющие реализовывать в интерфейсах поведение рассматриваемое как по умолчанию.

Класс, реализующий интерфейс, обязан реализовать все описанные в нём члены. Поэтому интерфейс является гарантией наличия описанных в нем характеристик у реализующего его объекта. Все члены, описанные в интерфейсе, неявно имеют модификатор доступа `public`. Интерфейс предназначен для описания _api_ или другими словами состояния и поведенея предназначенного для взвимодействия внешнего мира с объектом.



## Объявление (declaration)
________________

В _TypeScript_ интерфейс объявляется с помощью ключевого слова `interface` после которого указывается идентификатор за которым следует тело заключенное в фигурные скобки содержащие описание.

~~~~~typescript
interface Identifier {
    // тело интерфейса 
}
~~~~~

Объявление интерфейса возможно как в контексте модуля, так и в контексте функции или метода.

~~~~~typescript
interface Identifier {} // контекст модуля

class T {
    public method(): void {
        interface Identifier {} // контекст метода
    }
}

function func(): void {
   interface Identifier {} // контекст функции
}
~~~~~


## Конвенции именования интерфейсов
________________

Прежде чем продолжить, нужно обратить внимание на такой аспект, как конвенции именования интерфейсов. Существует два вида именования. 

Первый вид конвенций родом из языка _Java_ — они предлагают именовать интерфейсы точно так же, как и классы. Допускаются имена прилагательные.

~~~~~typescript
interface Identifier {}
~~~~~

Второй вид предлагает использовать конвенции языка _C#_, по которым интерфейсы именуются так же как классы, но с префиксом `I`, что является сокращением от _Interface_. Такой вид записи получил название _“венгерская нотация”_ в честь программиста венгерского происхождения, работавшего в компании _MicroSoft_. Допускаются имена прилагательные.

~~~~~typescript
interface IIdentifier {}
~~~~~

Чтобы сразу расставить все точки над i, стоит заметить, что в дальнейшем идентификаторы интерфейсов будут указываться по конвенциям _C#_.


## Реализация интерфейса (implements)
________________

Как уже было сказано в самом начале, все члены интерфейса являются открытыми (`public`) и их объявление не может содержать модификатор `static`. Кроме того, в _ypeScript_ интерфейсы не могут содержать реализацию.

Класс реализующий интерфейс обязан реализовывать его в полной мере. Любой класс, который хочет реализовать интерфейс должен указать это с помощью ключевого слова `implements`, после которого следует идентификатор реализуемого интерфейса. Указание реализации классом интерфейса располагается между идентификатором класса и его телом. 

~~~~~typescript
interface IAnimal {
    nickname: string;
    
    execute(command: string): void;
}

class Bird implements IAnimal {
    nickname: string;
    
    execute(command: string): void {}
}
~~~~~

Один класс может реализовывать сколько угодно интерфейсов. В этом случае реализуемые интерфейсы должны быть перечислены через запятую.

~~~~~typescript
interface IAnimal {}
interface IOviparous {} // указывает на возможность откладывать яйца

class Bird implements IAnimal, IOviparous {} 
~~~~~

В случае, когда класс расширяет другой класс, декларация реализации (`implements`) следует после декларации расширения (`extends`).

~~~~~typescript
interface IAnimal {}
interface IOviparous {} 

class Bird implements IAnimal, IOviparous {} 

interface IFlyable {}

class Eagle extends Bird implements IFlyable {}
~~~~~


## Декларация свойств get и set (accessors)
________________

Несмотря на то, что в интерфейсе можно декларировать поля и методы, в нем нельзя декларировать свойства `get` и `set` (_аксессоры_). Но, несмотря на это, задекларированное в интерфейсе поле может быть совместимо не только с полем, но и аксессорами. При этом нет разницы, будет в объекте объявлен _getter_, _setter_ или оба одновременно.

~~~~~typescript
interface IAnimal {
    id: string;
}

// только get
class Bird implements IAnimal {
    get id(): string {
        return 'bird';
    }
}

// только set
class Fish implements IAnimal {
    set id(value: string) {}
}

// и get и set
class Insect implements IAnimal {
    get id(): string {
     return 'insect';
    }

    set id(value: string) {}
}
~~~~~


## Указание интерфейса в качестве типа (interface types)
________________

Класс реализующий интерфейс принадлежит к типу этого интерфейса. Класс унаследованный от класса реализующего интерфейс, также наследует принадлежность к реализуемым им интерфейсам. В подобных сценариях говорят что класс наследует интерфейс.

~~~~~typescript
interface IAnimal {}

class Bird implements IAnimal {}

class Raven extends Bird {}

let bird: IAnimal = new Bird();
let raven: IAnimal = new Raven();
~~~~~

Класс, реализующий множество интерфейсов, принадлежит к типу каждого из них. Когда экземпляр класса реализующего интерфейс присваивают ссылке с типом интерфейса, то говорят что экземпляр был _ограничен_ типом интерфейса. То есть, функционал экземпляра класса урезается до описанного в интерфейсе (подробнее об этом речь пойдет в главе [“Типизация - Совместимость объектов”]() и [“Типизация - Совместимость функций”]()). 

~~~~~typescript
interface IAnimal {
    name: string;
}

interface IFlyable {
    flightHeight: number;
}

interface IIdentifiable {
    id: string;
}

class Animal implements IAnimal {
    constructor(readonly name: string) {}
}

class Bird extends Animal implements IFlyable {
    public flightHeight: number = 500;
}

var animal: IAnimal = new Bird('bird'); // экземпляр Bird ограничен до типа IAnimal
var fly: IFlyable = new Bird('bird'); // экземпляр Bird ограничен до типа IFlyable
~~~~~

Несмотря на то, что интерфейс является синтаксической конструкцией и может указываться в качестве типа, после компиляции от него не остается и следа. Это в свою очередь означает, что интерфейс, как тип данных, может использоваться только на этапе компиляции. Другими словами, компилятор сможет предупредить об ошибках несоответствия объекта описанному интерфейсу, но проверить на принадлежность к типу интерфейса с помощью операторов `typeof` или `instanceof` не получится поскольку они выполняются во время выполнения программы. Но в _TypeScript_ существует механизм (который будет рассмотрен далее в главе [“Типизация - Защитники типа”]()), позволяющий в некоторой мере решить эту проблему.


## Расширение интерфейсов (extends interface)
________________

Если множество логически связанных интерфейсов требуется объединить в один тип, то нужно воспользоваться механизмом расширения интерфейсов. Наследование интерфейсов осуществляется с помощью ключевого слова `extends`, после которого через запятую идет один или несколько идентификаторов расширяемых интерфейсов.

~~~~~typescript
interface IIdentifiable {}
interface ILiving {}

// интерфейсы IIdentifiable и ILiving вместе образуют логически связанную композицию, 
// которую можно выделить в тип интерфейс IAnimal
interface IAnimal extends IIdentifiable, ILiving {}
~~~~~

Для тех кто только знакомится с таким понятием как интерфейсы, будет не лишним узнать о _“Принципе разделения интерфейсов”_ (_Interface Segregation Principle_ или сокращенно _ISP_), который гласит, что более крупные интерфейсы нужно _“дробить”_ на более мелкие интерфейсы. Но нужно понимать, что условия дробления диктуются конкретным приложением. Если во всех случаях руководствоваться только принципами, то можно раздуть небольшое приложение до масштабов вселенной.

Для примера представьте приложение, которое только выводит в консоль информацию о животных. Так как над объектом `Animal` будет выполняться только одна операция, то можно не бояться разгневать богов объектно-ориентированного проектирования и включить все нужные характеристики прямо в интерфейс `IAnimal`.

~~~~~typescript
interface IAnimal {
    id: string;
    age: number;
}

class Animal implements IAnimal {
    public age: number = 0;
    
    constructor(readonly id: string) {}
}

class AnimalUtil {
    public static print(animal: IAnimal): void {
        console.log(animal);
    }
}

class Bird extends Animal {}

class Raven extends Bird {
    constructor() {
        super('raven');
    }
}

let raven: Raven = new Raven();

AnimalUtil.print(raven);
~~~~~

В такой программе, кроме достоинства архитектора, ничего пострадать не может, так как она выполняет только одну операцию вывода информации о животном.

Но если переписать программу, чтобы она выполняла несколько не связанных логически операций над одним типом, в данном случае `IAnimal`, то ситуация изменится на противоположную.

~~~~~typescript
interface IAnimal {/*...*/}

class Animal implements IAnimal {/*...*/}

class AnimalUtil {
    public static printId(animal: IAnimal): void {
        console.log(animal.id); // вывод  id
    }

    public static printAge(animal: IAnimal): void {
        console.log(animal.age); // вывод age
    }
}

class Bird extends Animal {}
class Raven extends Bird {/*...*/}

let raven: Raven = new Raven();

AnimalUtil.printId(raven);
AnimalUtil.printAge(raven);
~~~~~

В этом случае программа нарушает принцип _ISP_, так как статические методы `printId` и `printAge` получили доступ к данным, которые им не требуются для успешного выполнения. Это может привести к намеренной или по неосторожности порче данных.

~~~~~typescript
class AnimalUtil {
    public static printId(animal: IAnimal): void {
        // для успешного выполнения этого метода 
        // не требуется доступ к данным о animal.age
        console.log(animal.id);
    }

 public static printAge(animal: IAnimal): void {
        // для успешного выполнения этого метода 
        // не требуется доступ к данным о animal.id
        console.log(animal.age);
    }
}
~~~~~

Поэтому в подобных ситуациях настоятельно рекомендуется _“дробить”_ типы интерфейсов на меньшие составляющие и затем ограничивать ими доступ к данным.

~~~~~typescript
interface IIdentifiable {}
interface ILiving {}

interface IAnimal extends IIdentifiable, ILiving {/*...*/}

class Animal implements IAnimal {/*...*/}

class AnimalUtil {
    public static printId(animal: IIdentifiable): void {
        // параметр animal ограничен типом IIdentifiable
        console.log(animal.id);
    }

    public static printAge(animal: ILiving): void {
        // параметр animal ограничен типом ILiving
        console.log(animal.age);
    }
}

class Bird extends Animal {}
class Raven extends Bird {/*...*/}

let raven: Raven = new Raven();

AnimalUtil.printId(raven);
AnimalUtil.printAge(raven);
~~~~~


## Расширение интерфейсом класса (extends class)
________________

В случаях, когда нужно создать интерфейс для уже имеющегося класса, больше не нужно тратить силы на перечисление членов класса в интерфейсе. В _TypeScript_ интерфейсу достаточно расширить тип класса.

Когда интерфейс расширяет класс, он наследует описание членов, но не их реализацию.

~~~~~typescript
class Animal {
    nickname: string;
    age: number;
}

interface IAnimal extends Animal {}

class Bird implements IAnimal {
    nickname:string;
    age: number;
}

let bird: IAnimal = new Bird();
~~~~~

Но с расширением класса интерфейсом существует один нюанс.

Интерфейс полученный путем расширения типа класса может быть реализован только самим этим классом или его потомками, поскольку помимо публичных (`public`) также наследует закрытые (`private`) и защищенные (`protected`) члены.

~~~~~typescript
class Animal {
    private uid: string;
    protected maxAge: number;
    public name: string;
}

interface IAnimal extends Animal {}

class Bird extends Animal implements IAnimal { // Ok
    // private uid: string = ''; // Error, private
    protected maxAge: number = 100; // Ok, protected
    public name: string = 'bird'; // Ok,  public
}

class Fish implements IAnimal { // Error
    public name: string = 'fish';
}

let bird: IAnimal = new Bird(); // Ok
let fish: IAnimal = new Fish(); // Error
~~~~~


## Описание класса (функции-конструктора)
________________

Известный факт, что в _JavaScript_, а следовательно и в _TypeScript_, конструкция `class` - это лишь _“синтаксический сахар”_ над старой доброй функцией-конструктором. Эта особенность позволяет описывать интерфейсы не только для экземпляров класса, но и для самих классов (функций-конструкторов). Проще говоря, с помощью интерфейса можно описать как конструктор, так и статические члены класса, с одной оговоркой — этот интерфейс можно использовать только в качестве типа. То есть класс не может указывать реализацию такого интерфейса с помощью ключевого слова `implements` сопряженную с экземпляром, а не самим классом.

Описывать интерфейс для функции конструктора может потребоваться тогда, когда в качестве значения выступает сам класс.

Конструктор указывается с помощью ключевого слова `new`, затем открываются фигурные скобки в которых, при наличии, указываются параметры. В конце указывается тип возвращаемого значения.
 
~~~~~typescript
new(p1: type, p2: type): type;
~~~~~

Статические члены описываются также, как и обычные.

~~~~~typescript
interface IAnimal {
    nickname: string;
}

class Animal implements IAnimal {
    nickname: string;

    constructor(nickname: string) { 
        this.nickname = nickname;
    }
}

class Bird extends Animal {
    static DEFAULT_NAME: string = 'bird';

    static create(): IAnimal {
        return new Bird( Bird.DEFAULT_NAME);
    }
}

class Fish extends Animal {
    static DEFAULT_NAME: string = 'bird';
    
    static create(): IAnimal {
        return new Bird( Bird.DEFAULT_NAME);
    }
}

const bird: Bird = new Bird('bird');
const fish: Fish = new Fish('fish');

let a: IAnimal[] = [bird, fish]; // Ok, массив экземпляров классов реализующих интерфейс IAnimal
let b: IAnimal[] = [Bird, Fish]; // Error, массив классов

interface IAnimalConstructor { // декларация интерфейса для класса
    create(): IAnimal; // static method
    new (nickname: string): IAnimal; // конструктор
}

let c: IAnimalConstructor[] = [Bird, Fish]; // Ok, массив классов
let d: IAnimal[] = c.map(item => item.create()); // Ok, массив экземпляров классов реализующих интерфейс IAnimal
~~~~~


## Описание функционального выражения
________________

Помимо экземпляров и самих классов, интерфейсы могут описывать функциональные выражения. Это очень удобно, когда функциональный тип имеет очень большую сигнатуру, которая делает код менее читабельным. 

~~~~~typescript
// reduce(callbackfn: (previousValue: T, currentValue: T, currentIndex: number, array: T[]) => T, initialValue?: T): T;
var callback: (previusValue: number, currentValue: number, currentIndex: number, array: number[]) => number;
~~~~~

В большинство подобных случаев, можно прибегнуть к помощи вывода типов.

~~~~~typescript
// reduce(callbackfn: (previousValue: T, currentValue: T, currentIndex: number, array: T[]) => T, initialValue?: T): T;

var callback: (previusValue: number, currentValue: number, currentIndex: number, array: number[]) => number;
var callback = (previusValue: number, currentValue: number, currentIndex: number, array: number[]) => previusValue + currentValue;

let numberAll: number[] = [5, 5, 10, 30];

let sum: number = numberAll.reduce(callback); // 50
~~~~~

Но в случае, если функциональное выражение является параметром функции, как например метод массива `reduce`, то решением может служить только явная декларация типа.

~~~~~typescript
class Collection<T> {
    reduce(callbackfn: (previousValue: T, currentValue: T, currentIndex: number, array: T[]) => T, initialValue?: T): T {
        return null;
    }
}
~~~~~

Поэтому при необходимости указать тип явно, помимо рассмотренного в главе ["Типы - Type Queries (запросы типа), Alias (псевдонимы типа)"]() механизма создания псевдонимов типа (`type`), можно описать функциональное выражение с помощью интерфейса.

Для этого необходимо в теле интерфейса описать сигнатуру функции без указания идентификатора.

~~~~~typescript
interface ISumAll {
    (...valueAll: number[]): number;
}

const sumAll: ISumAll = (...valueAll: number[]) =>
    valueAll.reduce((result, value) => result += value, 0);


let numberAll: number[] = [5, 5, 10, 30];

let sum: number = sumAll(...numberAll);
~~~~~


## Описание индексных членов в объектных типов
________________

Индексные члены подробно будут рассматриваться в главе [“Типы - Объектные типы с индексными членами (объектный тип с динамическими ключами)”](), но не будет лишним и здесь коснутся этого механизма.

~~~~~typescript
interface IIndentifier  {
    [BindingIdentifier: string]: Type;
    [BindingIdentifier: number]: Type;
}
~~~~~


## Инлайн интерфейсы (Inline Interface)
________________

Помимо описания объекта, в конструкции объявляемой с помощью ключевого слова `interface`, тип объекта можно описать прямо в месте указания типа. Такой способ объявления типа неформально обозначается как _инлайн интерфейс_ (_)inline interface_). Всё ранее описанное для типов интерфейсов объявленных с помощью ключевого слова `interface`, в полной мере верно и для их инлайн аналогов.

Различие между обычным интерфейсом и инлайн интерфейсом в том, что второй обладает только телом и объявляется прямо в аннотации типа.

~~~~~typescript
let identifier: { p1: type, p2: type };
~~~~~

Интерфейс, объявленный с помощью ключевого слова `interface`, считается идентичным инлайн интерфейсу, если их описание совпадает. Но стоит обратить внимание, что это возможно благодаря структурной типизации, которая рассматривается в главе [“Экскурс в типизацию - Совместимость типов на основе вида типизации”]().

~~~~~typescript
interface IAnimal {
    nickname: string;
}

class Bird implements IAnimal {
    nickname: string;
}
class Fish implements IAnimal {
    nickname: string;
}

let bird: IAnimal = new Bird(); // Ok
let fish: { nickname: string } = new Fish(); // Ok
~~~~~

Как было сказано ранее, инлайн интерфейс можно объявлять в тех местах, в которых допускается указание типа. Тем не менее реализовывать (`implements`) и расширять (`extends`) инлайн интерфейс нельзя. 

~~~~~typescript
interface IT1{}
interface IT2{}

interface IT3 extends { f1: IT1, f2: IT2 } { // Error

}

class T4 implements { f1: T1, f2: T2 } { // Error

}
~~~~~

Хотя последнее утверждение и не совсем верно. В дальнейшем будет рассказано о такой замечательной конструкции, как обобщения (глава [“Типы - Обобщения (Generics)”]()), в которых, как раз таки возможно расширять (`extends`) инлайн интерфейсы.


## Слияние интерфейсов
________________

В случае, если в одной области видимости объявлено несколько одноимённых интерфейсов, то они будут объединены в один.

~~~~~typescript
// так видят разработчики
interface IAnimal {
    name: string;
}

interface IAnimal {
    age: number;
}

//так видит компилятор
/**
interface IAnimal {
    name: string;
    age: number;
}
*/

// разработчики получают то, что видит компилятор
let animal: IAnimal;
animal.name = 'animal'; // Ok
animal.age = 0; // Ok
~~~~~

При попытке переопределить тип поля, возникнет ошибка.

~~~~~typescript
interface IAnimal {
    name: string;
    age: number;
}

interface IAnimal {
    name: string; // Ok
    age: string; // Error
}
~~~~~

Если в нескольких одноимённых интерфейсах будут описаны одноимённые методы с разными сигнатурами, то они будут расценены, как описание перегрузки. К тому же, интерфейсы, которые описывают множество одноимённых методов, сохраняют свой внутренний порядок.

~~~~~typescript
interface IBird {}
interface IFish {}
interface IInsect {}
interface IReptile {}

// до компиляции
interface IAnimalFactory { 
    getAnimalByID(id: number): IBird;
}

interface IAnimalFactory {
    getAnimalByID(id: string): IFish;
}

interface IAnimalFactory {
    getAnimalByID(id: boolean): IInsect;
    getAnimalByID(id: object): IReptile;
}

/** при компиляции
interface IAnimalFactory { 
    getAnimalByID(id: string): IInsect;
    getAnimalByID(id: string): IReptile;
    getAnimalByID(id: string): IFish;
    getAnimalByID(id: string): IBird;
}
*/
let animal: IAnimalFactory;
let v1 = animal.getAnimalByID(0); // Ok -> v1: IBird
let v2 = animal.getAnimalByID('5'); // Ok -> v2: IFish
let v3 = animal.getAnimalByID(true); // Ok -> v3: IInsect
let v4 = animal.getAnimalByID({}); // Ok -> v4: IReptile
~~~~~

Исключением из этого правила являются сигнатуры, которые имеют в своем описании литеральные строковые типы данных (`literal String Types`). Дело в том, что сигнатуры содержащие в своем описании литеральные строковые типы, всегда размещаются перед сигнатурами, у которых нет в описании литеральных строковых типов.

~~~~~typescript
interface IBird {}
interface IFish {}
interface IInsect {}
interface IReptile {}

// до компиляции
interface IAnimalFactory { 
    getAnimalByID(id: string): IBird;
}

interface IAnimalFactory {
    getAnimalByID(id: 'fish'): IFish;
}

interface IAnimalFactory {
    getAnimalByID(id: 'insect'): IInsect;
    getAnimalByID(id: number): IReptile;
}

/** при компиляции
interface IAnimalFactory {
    getAnimalByID(id: 'fish'): IFish;
    getAnimalByID(id: 'insect'): IInsect;
    getAnimalByID(id: number): IReptile;
    getAnimalByID(id: string): IBird;
}
*/
~~~~~
