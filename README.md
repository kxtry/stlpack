<br>Example
<br>
<br>struct MyTest
<br>{
<br>	int i, j, k;
<br>	bool bval;
<br>	std::string txt;
<br>	std::vector&lt;short&gt; v;
<br>	std::list&lt;std::vector&lt;int&gt;&gt; c;
<br>	std::map&lt;std::string, std::vector&lt;int&gt;&gt; m;
<br>	std::map&lt;string, std::map&lt;std::string, std::vector&lt;int&gt;&gt; &gt; s;
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
<br>template&lt;typename T&gt;
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
<br>	std::vector&lt;int&gt; ca1, ca2;
<br>	ca1.push_back(8);
<br>	ca1.push_back(9);
<br>	ca2.push_back(10);
<br>	ca2.push_back(11);
<br>	t1.c.push_back(ca1);
<br>	t1.c.push_back(ca2);
<br>	t1.m.insert(std::map&lt;std::string,std::vector&lt;int&gt;&gt;::value_type("xyz", ca1));
<br>	t1.m.insert(std::map&lt;std::string,std::vector&lt;int&gt;&gt;::value_type("ijk", ca2));
<br>	t1.s.insert(std::map&lt;std::string,std::map&lt;std::string, std::vector&lt;int&gt;&gt;&gt;::value_type("opq", t1.m));
<br>	string txt;
<br>	t1.toString(txt);
<br>
<br>	t2.unString(txt);
<br>	return 0;
<br>}
