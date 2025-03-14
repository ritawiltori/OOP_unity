# oop unity


namespace oop
{
    internal class Program
    {
        static void Main(string[] args)
        {


            List<Spell> spells = new List<Spell>()
        {
            new Fireball(),
            new Healing(),
            new FrostNova()
        };


            Character target = new Character("Hero", 100, 50);

            foreach (Spell spell in spells)
            {
                spell.Cast(target);
                spell.DisplayInfo();
                Console.WriteLine($"Target Health: {target.Health}");
                Console.WriteLine($"Target Speed: {target.Speed}");
                Console.WriteLine();
            }

            Console.ReadLine();
        }
    }

    public class Character
    {
        public string Name { get; }
        public int Health { get; private set; }
        public int Speed { get; private set; }

        public Character(string name, int health, int speed)
        {
            Name = name;
            Health = health;
            Speed = speed;
        }

        public void TakeDamage(int damage)
        {
            Health -= damage;
            if (Health < 0) Health = 0;
        }

        public void Heal(int amount)
        {
            Health += amount;
        }

        public virtual void ReduceSpeed(int percent)
        {
            Speed -= (int)(Speed * (percent / 100.0f));
            if (Speed < 0) Speed = 0; 
        }
    }

    public abstract class Spell
    {
        public string Name { get; }
        public int Power { get; }

        protected Spell(string name, int power)
        {
            Name = name;
            Power = power;
        }

        public virtual void Cast(Character target)
        {
          
        }

        public virtual void DisplayInfo()
        {
            Console.WriteLine($"Spell Name: {Name}");
            Console.WriteLine($"Spell Power: {Power}");
        }
    }

    public class Fireball : Spell
    {
        public Fireball() : base("Fireball", 10) { }

        public override void Cast(Character target)
        {
            target.TakeDamage(Power);
            Console.WriteLine($"{Name} casted! {target.Name} takes {Power} damage.");
        }
    }

    public class Healing : Spell
    {
        public Healing() : base("Healing", 10) { }

        public override void Cast(Character target)
        {
            target.Heal(Power);
            Console.WriteLine($"{Name} casted! {target.Name} heals {Power} health.");
        }
    }

    public class FrostNova : Spell
    {
        public FrostNova() : base("Frost Nova", 10) { }

        public override void Cast(Character target)
        {
            target.TakeDamage(Power);
            target.ReduceSpeed(30);
            Console.WriteLine($"{Name} casted! {target.Name} takes {Power} damage and speed reduced.");
        }
    }
}


