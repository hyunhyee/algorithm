[문제링크] https://www.acmicpc.net/problem/1546

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);

		int N = sc.nextInt();
		double[] grades = new double[N];
		double max = 0, sum = 0;

		for (int i = 0; i < N; i++) {
			grades[i] = sc.nextInt();
			if (grades[i] > max)
				max = grades[i];
		}

		for (int i = 0; i < N; i++) {
			grades[i] = grades[i] / max * 100;
			sum += grades[i];
		}
		System.out.println(sum / N);
	}
