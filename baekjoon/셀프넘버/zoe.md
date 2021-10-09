[문제링크] https://www.acmicpc.net/problem/4673

	public static void main(String[] args) {
		boolean check[] = new boolean[10000];
		for (int i = 0; i < check.length; i++) {
			int n = d(i + 1);
			if (n < 10001) {
				check[n - 1] = true;
			}
		}
		for (int i = 0; i < check.length; i++) {
			if (check[i] == false) {
				System.out.println(i + 1);
			}
		}
	}

	static int d(int number) {
		int isSelfNumber = number;
		while (number != 0) {
			isSelfNumber = isSelfNumber + (number % 10);
			number = number / 10;
		}
		return isSelfNumber;
	}
