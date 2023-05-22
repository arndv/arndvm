// Citizens.And.Rebels


internal interface IBuyer

    {

        void BuyFood();

        int Food { get; }

    }



internal class Citizen : Community

    {

        private string birthdate;



        public string Birthdate { get => this.birthdate; set => this.birthdate = value; }



        public Citizen(string id, string name, int age, string birthdate) : base(id, name, age)

        {

            this.Birthdate = birthdate;

        }



        public override void BuyFood()

        {

            this.Food += 10;

        }



        public override string ToString()

        {

            return base.ToString() + $"Birthdate {this.Birthdate} Food: {this.Food}";

        }

    }



internal abstract class Community : IIdentifiable, IPersonable, IBuyer

    {

        private string id;

        private string name;

        private int age;

        private int food;



        public string Id { get => this.id; set => this.id = value; }

        public string Name { get => this.name; set => this.name = value; }

        public int Age { get => this.age; set => this.age = value; }

        public int Food { get => this.food; set => this.food = value; }



        protected Community(string id, string name, int age)

        {

            this.Id = id;

            this.Name = name;

            this.Age = age;

        }



        public abstract void BuyFood();



        public override string ToString()

        {

            return $"ID:{this.Id} {this.GetType().Name} Name: {this.Name} Age {this.Age} ";

        }

    }



 internal interface IIdentifiable

    {

        string Id { get; }

    }



internal interface IPersonable



    {

        string Name { get; }

        int Age { get; }



    }



internal class Program

{

    static void Main(string[] args)

    {

        int n = int.Parse(Console.ReadLine());



        Dictionary<string, Community> community = new Dictionary<string, Community>();



        for (int i = 0; i < n; i++)

        {

            string[] input = Console.ReadLine().Split();

            Community entity = CreateEntity(input);

            community.Add(input[0], entity);

        }



        string id = Console.ReadLine();

        while (id != "End")

        {

            if (community.ContainsKey(id))

            {

                community[id].BuyFood();

                Console.WriteLine(community[id]);

            }

            else

            {

                Console.WriteLine($"Entity with {id} does not exist!");

            }

            id = Console.ReadLine();

        }



        int totalFood = community.Sum(v => v.Value.Food);

        Console.WriteLine("TotalFood:" + totalFood);

    }



    public static Community CreateEntity(string[] info)

    {

        Community entity = null;

        string id = info[0];

        if (id.StartsWith("R"))

        {

            entity = new Rebel(id, info[1], int.Parse(info[2]), info[3]);

        }

        else if (id.StartsWith("C"))

        {

            entity = new Citizen(id, info[1], int.Parse(info[2]), info[3]);

        }

        return entity;

    }

}





internal class Rebel : Community

    {

        private string group;



        public string Group { get => this.group; set => this.group = value; }



        public Rebel(string id, string name, int age, string group) : base(id, name, age)

        {

            this.Group = group;

        }



        public override void BuyFood()

        {

            this.Food += 5;

        }



        public override string ToString()

        {

            return base.ToString() + $"Group {this.Group} Food: {this.Food}";

        }

    }
    
 //TEMA 7
 
1-ва задача:

using System;

namespace Sequence

{

class Program

{

static void Main(string[] args)

{

List<int> nums = Console.ReadLine().Split()

.Select(int.Parse) //1-ва грешка

.ToList();

int bestStart = 0; //2-ра грешка

int bestLength = 1;

int currentLength = 1;

int index = 0;

int first = nums[index];

for (int i = 1; i < nums.Count; i++)

{

if (first == nums[i])

{

currentLength++;

if (currentLength > bestLength)

{

bestLength = currentLength;

bestStart = index; //3-та грешка (трябваше да се добави)

}

}

else

{

currentLength = 1; //4-ta грешка (добавяме реда)

first = nums[i];

index = i;

}

}

for (int i = bestStart; i < bestStart + bestLength; i++)

{

Console.Write($"{nums[i]} ");

}

}

}

}

2-та задача (по първи вариант с пренаписване на решението):

class Program

{

static void Main(string[] args)

{

Stack<string> pages = new Stack<string>(); //1-ва промяна

string command = Console.ReadLine();

while (!"exit".Equals(command))

{

if (command.Equals("back"))

{

if (pages.Count != 0)

{

pages.Pop(); //изкарахме извикването на метода отгоре

Console.WriteLine(pages.Peek()); //маха от стека и връща резултата

}

}

else

{

//махаме иф-а

pages.Push(command); //добавяме в стека

}

command = Console.ReadLine();

}

}

}
    
    
    

2-та задача (с поправка на самия код):

class Program

{

static void Main(string[] args)

{

List<string> pages = new List<string>();

string command = Console.ReadLine();

while (!"exit".Equals(command))

{

if (command.Equals("back"))

{

if (pages.Count != 0)

{

pages.RemoveAt(pages.Count - 1); //изкарваме това тук

Console.WriteLine(pages.Last()); //премахваме елемента

}

}

else

{

//премахваме иф-а и previous променливата

pages.Add(command);

}

command = Console.ReadLine();

}

}

}
    
    
    

3-та задача:

class Program

{

static void Main(string[] args)

{

var list = Console.ReadLine().Split().Select(int.Parse).ToList();

for (int i = 0; i <= list.Count - 2; i++)

{

for (int j = 0; j <= list.Count - 2; j++) //сменяме името на променливата

{

if (list[j] > list[j + 1]) //сменяме посоката на знака, за да бъде във възходящ ред

{

//размяната НЕ беше наред...

(list[j], list[j + 1]) = (list[j + 1], list[j]);

}

}

}

Console.WriteLine(string.Join(" ", list));

}

}
    
    
    

4-та задача:

class Program

{

static void Main(string[] args)

{

var collection = Console.ReadLine().Split().Select(int.Parse).ToList(); //Readline -> ReadLine

for (int index = 0; index < collection.Count; index++)

{

int min = index;

for (int curr = index + 1; curr < collection.Count; curr++)

{

if (collection[curr] > collection[min])

{

min = curr;

}

}

int tmp = collection[index]; //добавяме променлива tmp

collection[index] = collection[min];

collection[min] = tmp; //променяме присвояването, така че да се присвоява tmp

}

Console.WriteLine(string.Join(" ", collection));

}

}

    
    
5-та задача:

class Program

{

static void Main(string[] args)

{

Stack<int> indexes = new Stack<int>(); //stack!

string expression = Console.ReadLine();

for (int i = 0; i < expression.Length; i++)

{

if (expression[i] == '(')

{

indexes.Push(i); //

}

else if (expression[i] == ')')

{

int startIndex = indexes.Pop(); //

int length = i - startIndex + 1;

string substr = expression.Substring(startIndex, length);

Console.WriteLine(substr);

}

}

}

}
                                      
                                      

6-та задача:

public T Pop()//2т

{

if (this.Count == 0)

{

throw new InvalidOperationException("Empty stack");

}

this.Count--;//2т

T element = this.items[this.Count];//2т

T[] temp = new T[this.items.Length];

for (int i = 0; i < this.Count; i++)

{

temp[i] = this.items[i];

}

this.items = temp;

return element;

}
 
 
    
//TEMA 8


CREATE DATABASE online_store;

USE online_store;

CREATE TABLE items (

item_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,

name VARCHAR(50) NOT NULL,

item_type_id INT NOT NULL,

FOREIGN KEY (item_type_id) REFERENCES item_types (item_type_id)

);

CREATE TABLE item_types (

item_type_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,

name VARCHAR(50) NOT NULL

);

CREATE TABLE order_items (

item_id INT NOT NULL,

order_id INT NOT NULL,

PRIMARY KEY (item_id, order_id),

FOREIGN KEY (item_id) REFERENCES items (item_id),

FOREIGN KEY (order_id) REFERENCES orders (order_id)

);

CREATE TABLE orders (

order_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,

customer_id INT NOT NULL,

FOREIGN KEY (customer_id) REFERENCES customers (customer_id)

);

CREATE TABLE customers (

customer_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,

name VARCHAR(50) NOT NULL,

birthday DATE NOT NULL,

city_id INT NOT NULL,

FOREIGN KEY (city_id) REFERENCES cities (city_id)

);

CREATE TABLE cities (

city_id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,

name VARCHAR(50) NOT NULL

);



    
//TEMA 9 
    
    
1. SELECT card_number, job_during_journey FROM travel_cards

ORDER BY card_number ASC;

2. SELECT id, CONCAT(first_name, ' ', last_name), ucn FROM colonists

ORDER BY first_name ASC, last_name ASC, id ASC;

3. SELECT s.name AS 'spaceship_name', sp.name AS 'spaceport_name' FROM spaceships AS s

INNER JOIN journey AS j ON s.id = j.spaceship_id

INNER JOIN spaceports AS sp ON sp.id = j.destination_spaceport_id

ORDER BY light_speed_rate DESC LIMIT 1;
    
    
// tema 15
    
    cd ~

mkdir mydir

cd mydir

mkdir colors shapes animals

cd animals

mkdir reptiles mammals

cd ../colors

touch red green blue

echo '#ff0000' > red

echo '#00ff00' > green

echo '#0000ff' > blue

cd ../../

zip -r mydir.zip mydir
    
    
//TEMA 16 Phyton
1задача
import math
import matplotlib.pyplot as plt
import numpy as np


a = np.array([ [1,2,5], [1, -1, 2], [3, -6, -1] ]) # 
b = np.array([-9,3,25]) #
x = np.linalg.solve(a,  b) #
print(x) # решение на системата: [ 2. -3. -1.]

2 задача
import matplotlib.pyplot as plt
import numpy as np
temperature = np.array([15, 13, 12, 12, 19, 22, 21, 18])
print(f'Средна дневна температура: {np.mean(temperature) }')
    
    
3 задача
import matplotlib.pyplot as plt
import numpy as np
temperature = np.array([15, 13, 12, 12, 19, 22, 21, 18])
hours = np.array(["0:00", "3:00", "6:00", "9:00", "12:00", "15:00", "18:00", "21:00"])
plt.plot(hours, temperature)
plt.xlabel('Час') #добавяме апострофи
plt.ylabel('Температура') #добавяме скобите
plt.title('Графика на температурата през дененощието')
plt.show() #добавяме скобите
    
    
4 задача
import numpy as np
data = []
for i in range(3): #добавихме 3 в скобите
    row = list(map(int, input().split())) #таб навътре
    data.append(row) #таб навътре
matrix = np.array(data)
n = float(input('Enter a number: '))
result = np.multiply(matrix, n) #multiply
print(result)
    
    
 5 задача
 import numpy as np
data = []
for i in range(2):
    row = list(map(int, input().split()))
    data.append(row)
matrix = np.array(data)
n = float(input('Enter a number: '))
result = np.multiply(matrix, n)
print(result)
    
    
//TEMA 16
    задача
    задача
    задача
    задача
