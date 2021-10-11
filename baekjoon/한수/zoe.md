[문제링크] https://www.acmicpc.net/problem/1065

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int n = sc.nextInt();
		int result = 0;

		for (int i = 1; i <= n; i++) {
			if (i < 100)
				result++;
			else if (i < 1000) {
				int hanRe = han(i);
				if (hanRe == 1) {
					result++;
				}
			}
		}
		System.out.println(result);
	}

	static int han(int n) {
		int hanRe = 0;
		int checkN = n;
		int first = checkN % 10;
		int second = (checkN / 10) % 10;
		int third = checkN / 100;
		if (third - second == second - first) {
			hanRe++;
		}
		return hanRe;
	}
