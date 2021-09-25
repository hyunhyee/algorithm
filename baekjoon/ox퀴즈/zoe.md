[문제링크] https://www.acmicpc.net/problem/8958

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		
		int N = sc.nextInt();
		String[] arrRe = new String[N];
		
		for (int i = 0; i < N; i++) {
		arrRe[i] = sc.next();
		}
		
		int count;
		int sum;
		
		for (int i = 0; i < arrRe.length; i++) {
			sum = 0;
			count = 0;
			char arrCheck[] = arrRe[i].toCharArray();
			for (int j = 0; j < arrCheck.length; j++) {
				if (arrCheck[j] == 'O') {
					count++;
					sum += count;
				} else {
					count = 0;
				}
			}
			System.out.println(sum);
		}
	}
