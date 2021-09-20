[문제링크] https://www.acmicpc.net/problem/2562

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		int seq = 0;
		int count = 0;
		int max = -100;
		int numbers[] = new int[9];

		for (int i = 0; i < numbers.length; i++) {
			numbers[i] = sc.nextInt();
			count++;
			if (numbers[i] > max) {
				max = numbers[i];
				seq = count;
			}
		}
		System.out.println(max);
		System.out.println(seq);
	}
