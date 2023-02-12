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
