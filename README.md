# BD_pilot
Задача 1. Напишите запрос, который выведет пилотов, которые в качестве второго пилота в августе этого года ездили в аэропорт Шереметьево.
use Pilot

select name
	from Pilot inner JOIN Raise on pilot_id=second_pilot_id 
	where destination = 'Шереметьево' and flight_dt > '2021-07-31' and flight_dt < '2021-09-01'
Задача 2. Выведите пилотов старше 45 лет, которые совершили больше 30 полетов на грузовых самолетах.
use Pilot

select Pilot.name
	from Raise inner JOIN Plane on Raise.plane_id = Plane.plane_id inner join Pilot on pilot_id=second_pilot_id or pilot_id=first_pilot_id
		where age > 44 and cargo_flg = 1 
		group by Pilot.name HAVING COUNT(cargo_flg) > 30
Задача 3. Выведите ТОП 10 пилотов-капитанов (first_pilot_id), которые перевезли наибольшее число пассажиров в этом году.
use Pilot

select top 10 Pilot.name, SUM(capacity)
	from Raise inner JOIN Plane on Raise.plane_id = Plane.plane_id inner join Pilot on pilot_id=first_pilot_id
		where  cargo_flg = 0 and flight_dt > '2020-12-31'
		group by Pilot.name
		order by SUM(capacity) DESC
Pilot-база данных
Pilot-табличка 1
Plane- табличка 2
Raise- табличка 3
