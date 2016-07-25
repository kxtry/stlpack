<br>Example

struct MyTest
{
	int i, j, k;
	bool bval;
	std::string txt;
	std::vector<short> v;
	std::list<std::vector<int>> c;
	std::map<std::string, std::vector<int>> m;
	std::map<string, std::map<std::string, std::vector<int>> > s;
	
	void toString(string& str) const
	{
		StlPack p;
		p << i << j << k << bval << txt << v << c << m << s;
		str = p.buffer();
	}
	
	void unString(const string& str)
	{
		StlUnpack up(str);
		up >> i >> j >> k >> bval >> txt >> v >> c >> m >> s;
	}
};

template<typename T>
int Test()
{
	MyTest t1, t2;
	t1.bval = true;
	t1.i = 2;
	t1.j = 3;
	t1.k = 4;
	t1.txt = "abc";
	t1.v.push_back(5);
	t1.v.push_back(6);
	t1.v.push_back(7);
	std::vector<int> ca1, ca2;
	ca1.push_back(8);
	ca1.push_back(9);
	ca2.push_back(10);
	ca2.push_back(11);
	t1.c.push_back(ca1);
	t1.c.push_back(ca2);
	t1.m.insert(std::map<std::string,std::vector<int>>::value_type("xyz", ca1));
	t1.m.insert(std::map<std::string,std::vector<int>>::value_type("ijk", ca2));
	t1.s.insert(std::map<std::string,std::map<std::string, std::vector<int>>>::value_type("opq", t1.m));
	string txt;
	t1.toString(txt);

	t2.unString(txt);
	return 0;
}
