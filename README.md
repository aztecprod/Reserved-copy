# Резервное копирование баз данных - Александр Шевцов
![image](https://github.com/aztecprod/Reserved-copy/assets/25949605/908bb74e-0e86-47e5-b8cd-8716e6144e5e)

1.1	Дифференциальное копирование, так как оно позволяет быстрее восстанавливать данные по сравнению с инкрементным резервным копированием, поскольку для этого требуется всего две части резервной копии: полная резервная копия и последняя дифференциальная резервная копия.

1.2	Инкрементное, так как оно может выполняться так часто, как требуется, ведь каждая новая копия не будет весить больше, чем предыдущая (если сравнивать с дифференциальным).

1.3	Да, если есть репликация master-slave

![image](https://github.com/aztecprod/Reserved-copy/assets/25949605/d76cc65e-b701-4041-8b55-04510e3d039f)

2.1 

# pg_-Fc dump my_bd > /tmp/my_bd.sql

# pg_restore -d my_bd /tmp/my_bd.sql

![image](https://github.com/aztecprod/Reserved-copy/assets/25949605/ffbe54d1-dd31-486a-8822-ab06d1ef8734)

3.1

1 способ:
mysqlbackup --defaults-file=/home/dbadmin/my.cnf --incremental --incremental-base=history:last_backup --backup-dir=/home/dbadmin/temp_dir --backup-image=incremental_image1.bi backup-to-image

2 способ (через утилиту Xtrabackup ):

Cначала создается полный бэкап, который потом станет отправной точкой для создания инкрементального бэкапа:

xtrabackup --backup --target-dir=/data/backups/full

Cоздание инкрементального бэкапа:

xtrabackup --backup --target-dir=/data/backups/inc1 --incremental-basedir=/data/backups/full 
