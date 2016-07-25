<br>Example
<br>
<br>struct MyTest
<br>{
<br>	int i, j, k;
<br>	bool bval;
<br>	std::string txt;
<br>	std::vector<short> v;
<br>	std::list<std::vector<int>> c;
<br>	std::map<std::string, std::vector<int>> m;
<br>	std::map<string, std::map<std::string, std::vector<int>> > s;
<br>	
<br>	void toString(string& str) const
<br>	{
<br>		StlPack p;
<br>		p << i << j << k << bval << txt << v << c << m << s;
<br>		str = p.buffer();
<br>	}
<br>	
<br>	void unString(const string& str)
<br>	{
<br>		StlUnpack up(str);
<br>		up >> i >> j >> k >> bval >> txt >> v >> c >> m >> s;
<br>	}
<br>};
<br>
<br>template<typename T>
<br>int Test()
<br>{
<br>	MyTest t1, t2;
<br>	t1.bval = true;
<br>	t1.i = 2;
<br>	t1.j = 3;
<br>	t1.k = 4;
<br>	t1.txt = "abc";
<br>	t1.v.push_back(5);
<br>	t1.v.push_back(6);
<br>	t1.v.push_back(7);
<br>	std::vector<int> ca1, ca2;
<br>	ca1.push_back(8);
<br>	ca1.push_back(9);
<br>	ca2.push_back(10);
<br>	ca2.push_back(11);
<br>	t1.c.push_back(ca1);
<br>	t1.c.push_back(ca2);
<br>	t1.m.insert(std::map<std::string,std::vector<int>>::value_type("xyz", ca1));
<br>	t1.m.insert(std::map<std::string,std::vector<int>>::value_type("ijk", ca2));
<br>	t1.s.insert(std::map<std::string,std::map<std::string, std::vector<int>>>::value_type("opq", t1.m));
<br>	string txt;
<br>	t1.toString(txt);
<br>
<br>	t2.unString(txt);
<br>	return 0;
<br>}
