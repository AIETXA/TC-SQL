
1 - SELECT * FROM sqlite_master;

## tbl_name : 
crime_scene_report, 
drivers_license,
facebook_event_checkin,
interview,
get_fit_now_member,
get_fit_now_check_in,
solution,
income,
person 


2- SELECT * FROM crime_scene_report;

3- SELECT *
   FROM crime_scene_report
   WHERE type = 'murder';

4- SELECT *
FROM crime_scene_report
WHERE type = 'murder'
AND city = 'SQL City'
AND date = '20180115';

date	    type	description	                                                                    city
20180115	murder	Security footage shows that there were 2 witnesses. 
                    The first witness lives at the last house on "Northwestern Dr". 
                    The second witness, named Annabel, lives somewhere on "Franklin Ave".	        SQL City

5- SELECT *
FROM person
WHERE address_street_name = 'Northwestern Dr'
ORDER BY address_number DESC
LIMIT 1; 

id	    name	        license_id	    address_number	    address_street_name	    ssn
14887	Morty Schapiro	118009	        4919	            Northwestern Dr	        111564949

SELECT *
FROM interview
WHERE person_id = 14887;

transcripción
Oí un disparo y luego vi a un hombre salir corriendo. Llevaba una bolsa de gimnasio "Get Fit Now". El número de socio empezaba por "48Z". Solo los socios Gold tienen esas bolsas. El hombre se subió a un coche con matrícula "H42W".

6- SELECT *
FROM person
WHERE name LIKE '%Annabel%'
AND address_street_name = 'Franklin Ave';    

id	    name	        license_id	    address_number	    address_street_name	    ssn
16371	Annabel Miller	490173	        103	                Franklin Ave	        318771143

SELECT *
FROM interview
WHERE person_id = 16371;

transcript
Vi ocurrir el asesinato y reconocí al asesino en mi gimnasio cuando estaba entrenando la semana pasada, el 9 de enero.

7- SELECT *
FROM drivers_license
WHERE plate_number LIKE '%H42W%'
AND gender = 'male';

id	    age	height	eye_color	hair_color	gender	plate_number	car_make	car_model
423327	30	70	    brown	    brown	    male	0H42W2	        Chevrolet	Spark LS
664760	21	71	    black	    black	    male	4H42WR	        Nissan	    Altima

8- SELECT *
FROM get_fit_now_check_in
WHERE check_in_date = 20180109
AND membership_id LIKE '%48Z%';

membership_id	check_in_date	check_in_time	check_out_time
48Z7A	        20180109	      1600	        1730
48Z55	        20180109	      1530	        1700

9- SELECT *
FROM get_fit_now_member
WHERE membership_status = 'gold'
AND id LIKE '%48Z%';

id	    person_id	name	        membership_start_date	membership_status
48Z7A	28819	    Joe Germuska	20160305	            gold
48Z55	67318	    Jeremy Bowers	20160101	            gold

10- SELECT p.*, dl.*
FROM person p
JOIN drivers_license dl
  ON p.license_id = dl.id
WHERE p.id IN (28819,67318);

id	name|license_id|address_number|address_street_name|ssn|id|age|height|eye_color|hair_color|gender|plate_number|car_make|car_model
67318|Jeremy Bowers|423327|530|Washington Pl, Apt 3A|871539279|423327|30|70|brown|brown|male|0H42W2|Chevrolet|Spark LS

11-INSERT INTO solution VALUES (1, 'Jeremy Bowers');
        
        SELECT value FROM solution;

¡Felicidades, encontraste al asesino! Pero espera, hay más... Si te sientes preparado para el reto, intenta consultar la transcripción de la entrevista del asesino para encontrar al verdadero villano detrás de este crimen. Si te sientes especialmente seguro con tus habilidades en SQL, intenta completar este último paso con un máximo de dos consultas. Usa la misma instrucción INSERT con tu nuevo sospechoso para comprobar tu respuesta.


## plus:

SELECT transcript
FROM interview
WHERE person_id = 67318;

transcripción
Me contrató una mujer con mucho dinero. No sé su nombre, pero sé que mide entre 1,65 y 1,70 m. Es pelirroja y conduce un Tesla Model S. Sé que asistió al concierto sinfónico de SQL tres veces en diciembre de 2017.


SELECT *
  FROM drivers_license
  WHERE hair_color = 'red'
  AND gender = 'female' AND car_make = 'Tesla' ;

  id	age	height	eye_color	hair_color	gender	plate_number	car_make	car_model
202298	68	66	    green	    red	        female	500123	        Tesla	    Model S
291182	65	66	    blue	    red	        female	08CM64	        Tesla	    Model S
918773	48	65	    black	    red	        female	917UU3	        Tesla	    Model S

SELECT person_id, COUNT(*) AS veces
FROM facebook_event_checkin
WHERE event_name = 'SQL Symphony Concert'
  AND date BETWEEN 20171201 AND 20171231
GROUP BY person_id
HAVING COUNT(*) = 3;

person_id	veces
24556	    3
99716	    3

SELECT person.id AS person_id,
       person.name,
       drivers_license.*
FROM person
JOIN drivers_license ON person.license_id = drivers_license.id
WHERE person.id IN (24556, 99716)
  AND hair_color = 'red'
  AND gender = 'female'
  AND car_make = 'Tesla'
  AND car_model = 'Model S';

person_id	name	            id	    age	height	eye_color	hair_color	gender	plate_number	car_make	car_model
99716	    Miranda Priestly	202298	68	66	    green	    red	        female	500123	        Tesla	    Model S

INSERT INTO solution VALUES (1, 'Miranda Priestly');
        
        SELECT value FROM solution;

¡Felicidades, encontraste al cerebro detrás del asesinato! En SQL City, todos te aclaman como el mejor detective de SQL de todos los tiempos. ¡Hora de descorchar el champán!