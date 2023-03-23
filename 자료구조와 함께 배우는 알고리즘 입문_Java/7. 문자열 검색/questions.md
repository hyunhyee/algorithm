[Q1]
```dart
class BFmatchEx {

	static int bfMatch(String txt, String pat) {abcdef / de
		int pt = 0;			
		int pp = 0;			
    
		int count = 0;	
		int k = -1;

		while (pt != txt.length() && pp != pat.length()) {  0 = 6 동시에 0 =2 아닐 때까지
			if (k == pt - pp)    -1 = 0-0 = 0             📍패턴이 텍스트보다 길면 공백을 넣어서 다음 진행 사이에 한칸 비우기
				System.out.print("    ");
			else {
<!-- 				System.out.printf("%2d  ", pt - pp);  ❓
				k = pt - pp;   k = -1 -> 0
			} 
      
			for (int i = 0; i < txt.length(); i++)
		        System.out.print(txt.charAt(i) + " "); 📍배열 txt에 있는 거 하나씩 출력
			System.out.println();                  📍한칸 내리고

			for (int i = 0; i < pt * 2 + 4; i++)     0*2+4 = 4 0<4
			System.out.print(" "); 📍d옆으로 한칸 띄고
			System.out.print(txt.charAt(pt) == pat.charAt(pp) ? '+' : '|'); 📍txt랑 pattern이랑 [0]인덱스 비교해서 같으면 + 아니면 |
			System.out.println(); 📍한칸 내리고

			for (int i = 0; i < (pt-pp) * 2 + 4; i++)  (0-0)*2 + 4  
				System.out.print(" ");            ❓한칸 띄기 * 오른쪽에 남은 개수

			for (int i = 0; i < pat.length(); i++) 📍패턴 길이만큼 
				System.out.print(pat.charAt(i) + " ");
			        System.out.println();
			        System.out.println();
			        count++;   ❓

			if (txt.charAt(pt) == pat.charAt(pp)) {
				pt++;
				pp++;
			} else {
				pt = pt - pp + 1;
				pp = 0;
			}
		}
		System.out.printf("비교를 %d회 했습니다.\n", count);
		if (pp == pat.length())		// 검색 성공
			return pt - pp;
		return -1;								
	}

	public static void main(String[] args) {
		if (idx == -1)
			System.out.println("텍스트에 패턴이 없습니다.");
		else {
			int len = 0;
			for (int i = 0; i < idx; i++)
				len += s1.substring(i, i + 1).getBytes().length;
			len += s2.length();

			System.out.println((idx + 1) + "번째 문자부터 일치합니다.");
			System.out.println("텍스트 : " + s1);
			System.out.printf(String.format("패  턴 : %%%ds\n", len), s2);
		}
	}
```

[Q2]
```dart
class BFmatchRev {
	static int bfMatchR(String txt, String pat) {
		int pt = txt.length() - 1;		
		int pp = pat.length() - 1;		

		while (pt >= 0 && pp >= 0) {
			if (txt.charAt(pt) == pat.charAt(pp)) {
				pt--;
				pp--;
			} else {
				pt = pt + (pat.length() - pp) - 2;
				pp = pat.length() - 1;
			}
		}
		if (pp < 0)					// 검색 성공
			return pt + 1;
		return -1;					// 검색 실패
	}
}


```

[Q3]
```dart
class KMPmatchEx {
     static int kmpMatch(String txt, String pat) {
      int pt = 1;										
      int pp = 0;								
      int count = 0;		
      
      int[] skip = new int[pat.length() + 1];
      int k = -1;

       // 건너뛰기표 작성
      skip[pt] = 0; ❓ skip[1] = 0
      while (pt != pat.length()) {
         if (k == pt - pp)
            System.out.print("    ");
         else {
            System.out.printf("%2d  ", pt - pp);
            k = pt - pp;
         } 
         for (int i = 0; i < txt.length(); i++)
            System.out.print(txt.charAt(i) + " ");
         System.out.println();

         for (int i = 0; i < pt * 2 + 4; i++)
         System.out.print(" ");
         System.out.print(txt.charAt(pt) == pat.charAt(pp) ? '+' : '|');
         System.out.println();

         for (int i = 0; i < (pt-pp) * 2 + 4; i++)
            System.out.print(" ");

         for (int i = 0; i < pat.length(); i++)
            System.out.print(pat.charAt(i) + " ");
         System.out.println();
         System.out.println();
         count++;
         if (pat.charAt(pt) == pat.charAt(pp))
            skip[++pt] = ++pp;
         else if (pp == 0)
            skip[++pt] = pp;
         else
            pp = skip[pp];
      }

      // 검색
      System.out.println("검색");
      pt = pp = 0;
      while (pt != txt.length() && pp != pat.length()) {
         if (k == pt - pp)
            System.out.print("    ");
         else {
            System.out.printf("%2d  ", pt - pp);
            k = pt - pp;
         } 
         for (int i = 0; i < txt.length(); i++)
            System.out.print(txt.charAt(i) + " ");
         System.out.println();

         for (int i = 0; i < pt * 2 + 4; i++)
            System.out.print(" ");
         System.out.print(txt.charAt(pt) == pat.charAt(pp) ? '+' : '|');
         System.out.println();

         for (int i = 0; i < (pt-pp) * 2 + 4; i++)
            System.out.print(" ");

         for (int i = 0; i < pat.length(); i++)
            System.out.print(pat.charAt(i) + " ");
         System.out.println();
         System.out.println();
         count++;
         if (txt.charAt(pt) == pat.charAt(pp)) {
            pt++;
            pp++;
         } else if (pp == 0)
            pt++;
         else
            pp = skip[pp];
      }

      System.out.printf("비교를 %d회 했습니다.\n", count);
      if (pp == pat.length())		// 패턴의 모든 문자를 대조
         return pt - pp;
      return -1;					
   }
```

[Q4]
```dart
class BMmatchEx {
	static int bmMatch(String txt, String pat) {
		int pt;								
		int pp;								
		int txtLen = txt.length();		// txt의 문자수
		int patLen = pat.length();		// pat의 문자수
		int[] skip = new int[Character.MAX_VALUE + 1];	// 건너뛰기 표
		int count = 0;  
		int k = -1;

		// 건너뛰기 표 작성
		for (pt = 0; pt <= Character.MAX_VALUE; pt++)
			skip[pt] = patLen;
		for (pt = 0; pt < patLen - 1; pt++)
			skip[pat.charAt(pt)] = patLen - pt - 1   // pt == patLen - 1
			
		// 검색
		while (pt < txtLen) {
			pp = patLen - 1;               // pat의 마지막 문자에 주목

			if (k == pt - pp)
				System.out.print("    ");
			else {
				System.out.printf("%2d  ", pt - pp);
				k = pt - pp;
			} 
			for (int i = 0; i < txt.length(); i++)
				System.out.print(txt.charAt(i) + " ");
			        System.out.println();

			for (int i = 0; i < pt * 2 + 4; i++)
				System.out.print(" ");
			        System.out.print(txt.charAt(pt) == pat.charAt(pp) ? '+' : '|');
			        System.out.println();

			for (int i = 0; i < (pt-pp) * 2 + 4; i++)
				System.out.print(" ");

			for (int i = 0; i < pat.length(); i++)
				System.out.print(pat.charAt(i) + " ");
		         	System.out.println();
			        System.out.println();
			        count++;

			while (txt.charAt(pt) == pat.charAt(pp)) {
				if (pp == 0)
					return pt;         // 검색 성공
				pp--;
				pt--;
				if (k == pt - pp)
					System.out.print("    ");
				else {
					System.out.printf("%2d  ", pt - pp);
					k = pt - pp;
				} 
				for (int i = 0; i < txt.length(); i++)
				System.out.print(txt.charAt(i) + " ");
				System.out.println();

				for (int i = 0; i < pt * 2 + 4; i++)
				System.out.print(" ");
				System.out.print(txt.charAt(pt) == pat.charAt(pp) ? '+' : '|');
				System.out.println();

				for (int i = 0; i < (pt-pp) * 2 + 4; i++)
					System.out.print(" ");

				for (int i = 0; i < pat.length(); i++)
				        System.out.print(pat.charAt(i) + " ");
				        System.out.println();
				        System.out.println();
				        count++;
			}
			pt += skip[txt.charAt(pt)];
		}
		return -1;									
	}
}
```
