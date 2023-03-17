CREATE OR REPLACE FUNCTION f_pulkovo3to6(
    x_in NUMBER,
    y_in NUMBER
)RETURN VARCHAR2 AS
    point_3 sde.st_geometry;
    point_wgs sde.st_geometry;
    point_6 sde.st_geometry;
    string VARCHAR2(50);
    string_out VARCHAR2(50);
    srid in NUMBER (4);
    srid_out NUMBER (4);
BEGIN
    IF
        y_in >= 5384980.0816
        AND y_in < 5615268.3294
    THEN srid_in := 3329;
    ELSIF
        y_in >= 6372215.4114
        AND y_in < 6628029.9150
    THEN srid_in := 3330;
    ELSIF
        y_in >= 7371412.8652
        AND y_in < 7628830.6536
    THEN srid_in := 3331;
    ELSIF
        y_in >= 8374393.4187
        AND y_in < 8625848.1185
    THEN srid_in := 3332;
    END IF;
    string := 'point (' || replace(y_in, ',','.') || ' ' || replace(x_in, ',', '.') || ')';
    point_3 := sde.st_pointfromtext(string, srid_in);
    point_wgs : sde.st_geometry_operators.st_transform_f(point_3, 4326);
    IF point_wgs.minx <= 18 THEN srid out := 3333; 
    ELSE srid out := 3334;
    END IF;
    point_6 := sde.st_geometry_operators.st_transform_f(point_3, srid_out);
    string_out := round(point_6.miny, 2) || ';' || round(point_6.minx, 2);
    RETURN string_out;
END