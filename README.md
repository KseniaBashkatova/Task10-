## Практическое задание №10
```Csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

using System;

namespace Practic_10
{
    public partial class SpaceShuttle
    {
        private double _fuelKg;
        private double _oxygenHours;
        private int _hullIntegrity;
        private const double FuelConsumptionRate = 2.5;

        public string ShuttleName { get; set; }

        // Добавлено публичное свойство для кислорода
        public double OxygenHours
        {
            get { return _oxygenHours; }
            set
            {
                if (value < 0) _oxygenHours = 0;
                else _oxygenHours = value;
            }
        }

        public double FuelKg
        {
            get { return _fuelKg; }
            set { _fuelKg = value < 0 ? 0 : value; }
        }

        public int HullIntegrity
        {
            get { return _hullIntegrity; }
            set
            {
                if (value < 0) _hullIntegrity = 0;
                else if (value > 100) _hullIntegrity = 100;
                else _hullIntegrity = value;
            }
        }

        public bool IsOperational
        {
            get { return _hullIntegrity > 15 && _oxygenHours > 0; }
        }

        public SpaceShuttle(string shuttleName, double fuelkg, double oxygenHours, int hullIntegrity)
        {
            ShuttleName = shuttleName;
            FuelKg = fuelkg;
            OxygenHours = oxygenHours;
            HullIntegrity = hullIntegrity;
        }
    }

    public partial class SpaceShuttle
    {
        public void ExecuteOrbitalBurn(double burnTimeSeconds, double thrustPower)
        {
            if (burnTimeSeconds <= 0 || thrustPower <= 0)
            {
                Console.WriteLine("Ошибка: время и мощность должны быть больше нуля.");
                return;
            }

            double fuelRequired = burnTimeSeconds * thrustPower * FuelConsumptionRate;

            if (FuelKg < fuelRequired)
            {
                Console.WriteLine("Ошибка: маневр не может быть выполнен, топлива недостаточно.");
                return;
            }

            // Добавлена логика успешного выполнения
            FuelKg -= fuelRequired;
            Console.WriteLine($"Маневр выполнен успешно. Потрачено {fuelRequired} кг топлива.");
            Console.WriteLine($"Остаток топлива: {FuelKg} кг.");
        }
    }

    // Добавляем class Program с точкой входа Main
    internal class Program
    {
        static void Main(string[] args)
        {
            // Создаем рабочий шаттл
            var discovery = new SpaceShuttle("Discovery", 1000, 50, 90);

            // Пытаемся выполненить маневр, на который топлива хватит
            discovery.ExecuteOrbitalBurn(10, 5);
            // 10 * 5 * 2.5 = 125 кг. В шаттле 1000 кг. Маневр пройдет успешно.

            Console.WriteLine();

            // Пытаемся выполненить маневр, на который топлива не хватит
            discovery.ExecuteOrbitalBurn(500, 10);
            // 500 * 10 * 2.5 = 12500 кг. В шаттле осталось 875 кг. Будет ошибка.
        }
    }
}
```
### Результат выполнения:
<img width="1431" height="847" alt="1" src="https://github.com/user-attachments/assets/c55fc53b-35e3-42bc-b7a6-fc990b2420de" />
<img width="1430" height="840" alt="2" src="https://github.com/user-attachments/assets/3c208456-3f16-4641-873e-2638f4dffd50" />
<img width="1434" height="840" alt="3" src="https://github.com/user-attachments/assets/1e84c85f-c366-4429-aab2-3403b7300864" />
// Делал Аристов Максим
