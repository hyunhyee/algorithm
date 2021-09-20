[문제링크] https://www.acmicpc.net/problem/2577 </br>
[블로그] https://zoe21.tistory.com/269

#1

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int result = (sc.nextInt() * sc.nextInt() * sc.nextInt());
		int check[] = new int[10];
  
		while (result > 0) {
			check[result % 10]++; 
			//1의 자리의 숫자를 검사 -> 배열에 개수를 +1 ex) 1의 자리 수: 0 -> 배열 result[0]을 +1
			result /= 10;
			// 10으로 나눠서 일의 자리를 지운다
		}
		for (int i = 0; i < check.length; i++) {
			System.out.println(check[i]);
		}
	}
                                     
#2

 	public static  void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		int A = sc.nextInt();
		int B = sc.nextInt();
		int C = sc.nextInt();
		int multiply = A * B * C;

		String result = Integer.toString(multiply);
		char[] arrRe = result.toCharArray();

		int check[] = new int[10];

		for (int i = 0; i < check.length; i++) {
			for (int j = 0; j < arrRe.length; j++) {
				if (Character.forDigit(i, 10) == arrRe[j]) {
					check[i]++;
				}
			}
			System.out.println(check[i]);
		}
	}   
