#include <iostream>
#include <string>
#include <vector>

struct sequipo
{
    std::string nombre;
    int PJ;
    int PG;
    int PP;
    int PE;
    int DG;
    int PTS;
};

void jugar_partido(sequipo &X, sequipo &Y);
void mostrar_tabla(const std::vector<sequipo> &equipos);

int main()
{
    std::vector<sequipo> equipos(3);

    //Inicializando datos
    equipos[0].nombre = "Equipo A";
    equipos[1].nombre = "Equipo B";
    equipos[2].nombre = "Equipo C";
    
    for (sequipo &equipo : equipos)
    {
        equipo.PJ = 0;
        equipo.PG = 0;
        equipo.PP = 0;
        equipo.PE = 0;
        equipo.DG = 0;
        equipo.PTS = 0;
    }

    mostrar_tabla(equipos); 

    jugar_partido(equipos[0],equipos[1]);
    jugar_partido(equipos[1],equipos[2]);
    jugar_partido(equipos[2],equipos[0]);

    mostrar_tabla(equipos); 
    return 0;
}


void jugar_partido(sequipo &X, sequipo &Y)
{
    int goles_x,goles_y;
    char letra_equipo_X = X.nombre[7];
    char letra_equipo_Y = Y.nombre[7];  
 
    std::cout<<"Partido "<<X.nombre<<" vs "<<Y.nombre<<std::endl;
    std::cout<<"Ingrese goles de "<<letra_equipo_X<<": "<<std::endl;
    std::cin>>goles_x;
    std::cout<<"Ingrese goles de "<<letra_equipo_Y<<": "<<std::endl;
    std::cin>>goles_y;
    //Ambos juegan 1 partido
    X.PJ++;
    Y.PJ++;
    //Diferencia de goles
    X.DG += goles_x-goles_y;
    Y.DG += goles_y-goles_x;
    //Partido ganados, perdidos o empatados
    if (goles_x>goles_y)
    {
        X.PG++;
        Y.PP++;
        X.PTS+=3;
    }
    else if (goles_x<goles_y)
    {
        Y.PG++;
        X.PP++;
        Y.PTS+=3;
    }
    else
    {
        X.PE++;
        Y.PE++;
        X.PTS++;
        Y.PTS++;
    }
};

void mostrar_tabla(const std::vector<sequipo> &equipos)
{
    std::cout<<" ---------------- REUSLTADOS --------------- "<<std::endl;
    std::cout<<"EQUIPO\t\t"<<"PJ\t"<<"PG\t"<<"PP\t"<<"PE\t"<<"DG\t"<<"PTS\t"<<std::endl;
    for (sequipo equipo : equipos)
        std::cout<<equipo.nombre<<"\t"<<equipo.PJ<<"\t"<<equipo.PG<<"\t"<<equipo.PP<<"\t"<<equipo.PE<<"\t"<<equipo.DG<<"\t"<<equipo.PTS<<"\t"<<std::endl;

};
