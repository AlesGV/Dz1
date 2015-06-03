#include "stdafx.h"
#include <iostream>
#include <string>
#include <list>
#include <algorithm>
#include <typeinfo>
#include <vector>
using namespace std;

class Home // абстрактный базовый класс
{
	private:
		string home_number; // число домов
		int    i_home_number; // число домов (целый тип)
		int    EtagCount; // количеcтво этажов
		int    MenCount;      // количество человек
		bool   HomeRemont; // ремонт дома
		int    NumbApartament;  // количество квартир 
		
	public:
		
		Home(){}// конструктор по умолчанию
		Home(Home & H)// констуктор копирования 
		{
			home_number    = H.home_number;
			i_home_number  = H.i_home_number;
			EtagCount      = H.EtagCount;
			MenCount       = H.MenCount;
			HomeRemont     = H.HomeRemont;
			NumbApartament = H.NumbApartament;	
		} 
		Home(string home_num,int i_home_num,int etag_count,int men_count,bool home_remont,int num_apartament) // конструктор со всема параметрами 
		{
			home_number    = home_num;
			i_home_number  = i_home_num;
			EtagCount	   = etag_count;
			MenCount	   = men_count ;
			HomeRemont	   = home_remont;
			NumbApartament = num_apartament;
		}

		~Home(){}// деструктор
		
		virtual void PrintClass() =0;// виртуальные чистыем методы , если они  =0 это означает что класс абстрактный 
		virtual void NameClass() =0;

		// методы доступа до данных
		string getHomeNumber()	  {return home_number;    }
		int    getI_Home_Number() {return i_home_number;  }
		int    getEtagCount()	  {return EtagCount;      }
		int    getMenCount()	  {return MenCount;		  }
		bool   getHomeRemont()    {return HomeRemont;     }
		int    getNumApartament() {return NumbApartament; }
		// что бы задать отдельно количество крватир или количесвто человек используем эти методы доступа
		void    setHomeNumber(string s)	  {home_number    = s; }
		void    setI_Home_Number(int i)   {i_home_number  = i; }
		void    setEtagCount(int i)	      {EtagCount      = i; }
		void    setMenCount(int i)	      {MenCount       = i; }
		void    setHomeRemont(bool i)     {HomeRemont     = i; }
		void    setNumApartament(int i)   {NumbApartament = i; }


};


class Street : public Home // другой клас наследует абстрактрактный , абстрактный класс в наем случае есть интерфейс
{
	private:// все закритые данные
		string Name_Street;
		int    Homes_num;
		int    NumberStreet;
		bool   Remont;
		list<Street> lis_street;//что бы не создавать класс список за основу берем список из стандартной библиотеки stl
	public:
		Street(){Name_Street = "";}// конструктор по умолчанию
		Street( string name)            {Name_Street =  name;}// коструктор с одним параметром
		Street( string sName , int Num) {Name_Street = sName; NumberStreet = Num;}
		Street(Street & S){Name_Street = S.Name_Street; Homes_num = S.Homes_num; NumberStreet = S.NumberStreet; Remont = S.Remont;}// конструктор компирования 
		// методы доступа до данных
		string getNameStreet()	   {return Name_Street;  }
		int    getHomes_num()	   {return Homes_num;    }
		int    getNumberStreet()   {return NumberStreet; }
		bool   getRemont()		   {return Remont;		 }

		void   setNameStreet(string s)	   {Name_Street  = s; }
		void   setHomes_num(int i)	       {Homes_num    = i; }
		void   setNumberStreet(int i)      {NumberStreet = i; }
		void   setRemont(bool i)		   {Remont       = i; }

	
		virtual void NameClass(){ cout << "Class Street " << endl;} // переопределение метода из абстрактного класса 

		void Input_Data()// ввод данных 
		{
			int n;string s;
			Street street;// этот обект будем добавлять в список 
			bool rem;
			cout <<"Введите номер дома "  << endl;
			cin >> n;
			street.setI_Home_Number(n);
			//cout << street.getI_Home_Number() << endl;;
			cout <<"Число этажей в доме " << endl;
			cin >> n;
			street.setEtagCount(n);
			cout << "Число жителей в доме "	<< endl;

			cin >> n;
			street.setMenCount(n);
			cout <<"Ремонт (1/0) " << endl;
			cin >> rem;
			street.setHomeRemont(rem);
			cout << "Число квартир в доме " << endl;
			cin >> n;
			street.setNumApartament(n);
			cout <<"Название улицы " << endl;
			cin.get();
			getline(cin,s);
			street.setNameStreet(s);
			cout <<"Число домов на улице" << endl;
			cin >> n;
			street.setHomes_num(n);
			cout <<"Номер улицы" << endl;
			cin >> n;
			street.setNumberStreet(n);
			cout <<"Признак ремонта домов на улице " << endl;
			cin >> rem;
			street.setRemont(rem);
			lis_street.push_back((Street)street);
			// вывод информации 
			       cout <<"вся сохраненная информация" << endl;
			        cout << "Номер "								   << street.getI_Home_Number() << endl;
					cout << "Число этажей в доме "                     << street.getEtagCount()     << endl;
					cout << "Число жителей в доме "					   << street.getMenCount()      << endl;
					cout << "Ремонт (1 - не требуется, 0 - требуется) "<< street.getHomeRemont()    << endl;
					cout << "Число квартир в доме "					   << street.getNumApartament() << endl;
					cout << "название улицы "						   << street.getNameStreet()    << endl;
					cout << "Число домов на улице "					   << street.getHomes_num()	    << endl;
					cout << "Номер улицы "							   << street.getNumberStreet()  << endl;
					cout << "Признак ремонта домов на улице "          << street.getRemont ()       << endl;

			
		}


	 void PrintClass()// переопределенный метод из абстрактного класса для вывода информации 
		{
				cout <<"вся сохраненная информация" << endl;
				for(auto i = lis_street.begin(); i != lis_street.end(); i++)
				{ 
					cout << "Номер "								   << i->getI_Home_Number() << endl;
					cout << "Число этажей в доме "                     << i->getEtagCount()     << endl;
					cout << "Число жителей в доме "					   << i->getMenCount()      << endl;
					cout << "Ремонт (1 - не требуется, 0 - требуется) "<< i->getHomeRemont()    << endl;
					cout << "Число квартир в доме "					   << i->getNumApartament() << endl;
					cout << "название улицы "						   << i->getNameStreet()    << endl;
					cout << "Число домов на улице "					   << i->getHomes_num()	    << endl;
					cout << "Номер улицы "							   << i->getNumberStreet()  << endl;
					cout << "Признак ремонта домов на улице "          << i->getRemont ()       << endl;
				}
		}


};

int main()
{
	setlocale(LC_ALL,"Rus");
	Street str;// создали обект 
	str.NameClass();// показали имя класса 
	str.Input_Data();// ввод инофрмации и вывод на экран

	cin.get();
	cin.get();

	return 0;
}
