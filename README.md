Файл main.c содержит реализацию 1-го этапа задания (OpenMP-программа).
При комментировании #pragma и запуска командной строки без указания количества нитей, программа выполняет последовательный код.
Количество нитей задается через параметр OMP_NUM_THREADS при запуске программы.
Компиляция: gcc main.c -lm -fopenmp -o a.out
Запуск: bsub -o result -e resultErr OMP_NUM_THREADS=K ./a.out - для K нитей, где K>1
Размер сетки и точность алгоритма задается в коде программы (переменные M, N, delta соответственно).

Файл main_mpi.c содержит реализацию 2-го этапа задания (MPI-программа).
Компиляция: mpixlc -lm main.c
Запуск: bsub -o 40x40.out -e 40x40.err -R "affinity[core(K)]"\ -n K -m "polus-c4-ib" mpiexec -n K ./a.out,
где 'K' - количество процессов.
Размер сетки и точность алгоритма задается в коде программы (переменные M, N, delta соответственно).

В папке MPI_OpenMP находятся три папки: 40х40, 80х90, 160х180 для каждой из сеток соответственно.
- Папка 40х40 содержит код для запуска гибридной реализации для сетки 40х40 main_openMP_MPI.c и makefile, в котором:
compile - компиляция программы;
submit_40_40_K_L - запуск программы с K нитями и с L процессами. В данном makefile все вариации комбинаций от 1 до 4 процессов и нитей.
- Папка 80х90 содержит код для запуска гибридной реализации для сетки 80х90 main_openMP_MPI.c и makefile, в котором:
compile - компиляция программы;
submit_80_90_K_L - запуск программы с K нитями и с L процессами.
Содержит запуски для количества нитей и процессов в соответствии с заданием, а также несколько тестовых вариаций сочетания.
- Папка 160х180 содержит код для запуска гибридной реализации для сетки 160х180 main_openMP_MPI.c и makefile, в котором:
compile - компиляция программы;
submit_160_180_K_L - запуск программы с K нитями и с L процессами.
Содержит запуски для количества нитей и процессов в соответствии с заданием.