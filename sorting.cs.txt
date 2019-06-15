using System;
using System.Collections.Generic;
using System.Linq;

class sortingprogram
{
	static void Main(String[] args)
	{

        // Input will never have values outside of the range of 0 to 255
		var input = "04,29,244,201,222,49,1,4,4,4,5,8,4,4,2,2,2,1,87";
        
		var expectedAscending = "1,1,2,2,2,4,4,4,4,4,4,5,8,29,49,87,201,222,244";
		var expectedDescending = "244,222,201,87,49,29,8,5,4,4,4,4,4,4,2,2,2,1,1";
		
		var ascendingResult = Sort(input, true);
		var descendingResult = Sort(input, false);

		Console.WriteLine(ascendingResult);
		Console.WriteLine(ascendingResult == expectedAscending);

		Console.WriteLine(descendingResult);
		Console.WriteLine(descendingResult == expectedDescending);
        
	}

	static string Sort(string input, bool isAscending)
	{
		if (string.IsNullOrWhiteSpace(input)) 
            return input;

        byte numberToSet; 
        List<byte> unsortedlist= new List<byte>();

        foreach(string str in input.Split(','))
        {
            if(byte.TryParse(str,out numberToSet))
            {
               numberToSet = Convert.ToByte(str);
                if(numberToSet <= (int)Byte.MaxValue && numberToSet >= (int)Byte.MinValue)
                {
                 unsortedlist.Add(numberToSet);
                }
            }
        }

        if(unsortedlist==null)
           return string.Empty;

        string result="";

        if(isAscending)
            unsortedlist = unsortedlist.OrderBy(x=>x).ToList();
        else 
            unsortedlist = unsortedlist.OrderByDescending(a=>a).ToList();
        
        foreach(var v in unsortedlist)
          result+= v.ToString() + ",";

        result = result.TrimEnd(',');

        return result;
    }
}
