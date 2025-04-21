# Codigo sel cursor

DELIMITER //

CREATE PROCEDURE cursor_simple()
BEGIN
    DECLARE hecho INT DEFAULT 0;
    DECLARE numero INT;
    DECLARE cur CURSOR FOR 
        SELECT 1 UNION ALL SELECT 2 UNION ALL SELECT 3 UNION ALL SELECT 4 UNION ALL SELECT 5;
    DECLARE CONTINUE HANDLER FOR NOT FOUND SET hecho = 1;

    OPEN cur;

    bucle: LOOP
        FETCH cur INTO numero;
        IF hecho THEN 
            LEAVE bucle;
        END IF;

        SELECT CONCAT('Número: ', numero) AS resultado;
    END LOOP;

    CLOSE cur;
END //

DELIMITER ;


call cursor_simple();

