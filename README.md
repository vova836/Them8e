using System;
using System.Collections.Generic;

class Address
{
    public string City { get; set; }
    public string Street { get; set; }
    public int HouseNumber { get; set; }
    public int ApartmentNumber { get; set; }
    public string PhoneNumber { get; set; }
    public List<string> Tenants { get; set; }
}

class Program
{
    static void Main()
    {
        List<Address> addresses = new List<Address>();

        // Создаем 10 адресов
        for (int i = 0; i < 10; i++)
        {
            Address address = new Address();
            address.City = "Город " + i.ToString();
            address.Street = "Улица " + i.ToString(); // Мы предполагаем, что названия улиц могут быть изменены, поэтому добавляем индекс в конец
            address.HouseNumber = i + 1;
            address.ApartmentNumber = i * 2;
            address.PhoneNumber = "(999) 123-456" + i.ToString();
            address.Tenants = new List<string> { "Фамилия" + i.ToString(), "Имя" + i.ToString(), "Отчество" + i.ToString() };
            addresses.Add(address);
        }

        Console.WriteLine("Введите запрос (1 - по заданной фамилии, имени, отчеству; 2 - по заданному адресу; 3 - по номеру телефона):");
        int choice = Convert.ToInt32(Console.ReadLine());

        switch (choice)
        {
            case 1:
                Console.WriteLine("Введите фамилию, имя и отчество через пробел:");
                string[] input1 = Console.ReadLine().Split(' ');
                string lastName = input1[0];
                string firstName = input1[1];
                string middleName = input1[2];
                foreach (var address in addresses)
                {
                    if (address.Tenants[0] == lastName && address.Tenants[1] == firstName && address.Tenants[2] == middleName)
                    {
                        Console.WriteLine($"Адрес: {address.City}, {address.Street}, {address.HouseNumber}, {address.ApartmentNumber}");
                    }
                }
                break;

            case 2:
                Console.WriteLine("Введите город, улицу и номер дома через пробел:");
                string[] input2 = Console.ReadLine().Split(' ');
                string city = input2[0];
                string street = input2[1];
                int houseNumber = Convert.ToInt32(input2[2]);
                foreach (var address in addresses)
                {
                    if (address.City == city && address.Street == street && address.HouseNumber == houseNumber)
                    {
                        Console.WriteLine($"Жильцы: {address.Tenants[0]} {address.Tenants[1]} {address.Tenants[2]}");
                    }
                }
                break;

            case 3:
                Console.WriteLine("Введите номер телефона:");
                string phoneNumber = Console.ReadLine();
                foreach (var address in addresses)
                {
                    if (address.PhoneNumber == phoneNumber)
                    {
                        Console.WriteLine($"Адрес: {address.City}, {address.Street}, {address.HouseNumber}, {address.ApartmentNumber}");
                        Console.WriteLine($"Жильцы: {address.Tenants[0]} {address.Tenants[1]} {address.Tenants[2]}");
                    }
                }
                break;

            default:
                Console.WriteLine("Некорректный выбор.");
                break;
        }
    }
}
