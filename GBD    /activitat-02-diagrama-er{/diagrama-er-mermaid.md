``` mermaid
erDiagram
Enemic {
    string Codi PK "NOT NULL"
    string Nom "NOT NULL"
    string Tipus "NOT NULL"
    int Nivell "NOT NULL"
    int Vida
    int Força
    int Agilitat
    int Carisma
}
HABILITAT{
    string Codi PK "NOT NULL"
    string Nom "NOT NULL"
    float Cost
    int Dany
    int Cooldown
    string Tipus "NOT NULL"
}
PERSONATGE{
    string DNI PK "NOT NULL"
    string Nom "NOT NULL"
    string Cognom
    int Vida
    int Força
    int Agilitat
    int Carisma
}
MASCOTA {
    string NumChip PK "NOT NULL"
    string Nom "NOT NULL"
    string Motxilla
}
ITEM {
    string  Codi PK "NOT NULL"
    string Nom "NOT NULL"
    boolean Equipable
    boolean Comerciable
    string Tipus "NOT NULL"
    float Pes "NOT NULL"
    string Qualitat "NOT NULL"
    float MesuraX "NOT NULL"
    float MesuraY "NOT NULL"
    float MesuraZ "NOT NULL"
}

Enemic }O--O{ HABILITAT : Enfronta
Enemic }O--o{ PERSONATGE : Enfronta
HABILITAT }o--o{ HABILITAT : "Combina amb"
HABILITAT }O--O{ PERSONATGE : Poseeix
PERSONATGE ||--|| MASCOTA : Acompanya
PERSONATGE }O--O{ ITEM : Equipa 
MASCOTA }o--o{ ITEM : Carrega
``
