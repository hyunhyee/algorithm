[문제링크] https://www.acmicpc.net/problem/4344

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int c = sc.nextInt();

		for (int i = 0; i < c; i++) {
			int N = sc.nextInt();
			double[] arrGrades = new double[N];
			double sum = 0, average = 0, passScore = 0;

			for (int j = 0; j < N; j++) {
				arrGrades[j] = sc.nextInt();
				sum += arrGrades[j];
			}
			average = sum / N;

			for (int j = 0; j < N; j++) {
				if (arrGrades[j] > average) {
					passScore++;
				}
			}
			System.out.printf("%.3f%%\n", (passScore / N) * 100);
		}
	}
