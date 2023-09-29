#define LPP_LUMINOSITY          101     // 2 bytes, 1 lux unsigned
#define LPP_PRESENCE            102     // 1 byte, 1
#define LPP_TEMPERATURE         103     // 2 bytes, 0.1°C signed
#define LPP_RELATIVE_HUMIDITY   104     // 1 byte, 0.5% unsigned
#define LPP_ACCELEROMETER       113     // 2 bytes per axis, 0.001G
#define LPP_BAROMETRIC_PRESSURE 115     // 2 bytes 0.1 hPa Unsigned
#define LPP_GYROMETER           134     // 2 bytes per axis, 0.01 °/s
#define LPP_GPS                 136     // 3 byte lon/lat 0.0001 °, 3 bytes alt 0.01m


// Data ID + Data Type + Data Size
#define LPP_LUMINOSITY_SIZE          4
#define LPP_PRESENCE_SIZE            3
#define LPP_TEMPERATURE_SIZE         4
#define LPP_RELATIVE_HUMIDITY_SIZE   3
#define LPP_ACCELEROMETER_SIZE       8
#define LPP_BAROMETRIC_PRESSURE_SIZE 4
#define LPP_GYROMETER_SIZE           8
#define LPP_GPS_SIZE                 11

int MAX_SIZE  = 200;
class CayenneLPP {
    public:
        CayenneLPP(uint8_t size);
        ~CayenneLPP();
        
        void reset(void);
        uint8_t getSize(void);
        uint8_t* getBuffer(void);
        uint8_t copy(uint8_t* buffer);
        
        uint8_t addLuminosity(uint8_t channel, uint16_t lux);
        uint8_t addPresence(uint8_t channel, uint8_t value);
        uint8_t addTemperature(uint8_t channel, float celsius);
        uint8_t addRelativeHumidity(uint8_t channel, float rh);
        uint8_t addAccelerometer(uint8_t channel, float x, float y, float z);
        uint8_t addBarometricPressure(uint8_t channel, float hpa);
        uint8_t addGyrometer(uint8_t channel, float x, float y, float z);
        uint8_t addGPS(uint8_t channel, float latitude, float longitude, float meters);
    
    private:
        uint8_t *buffer;
        uint8_t maxsize;
        uint8_t cursor;
        
        
};

CayenneLPP Payload(MAX_SIZE);

CayenneLPP::CayenneLPP(uint8_t size) : maxsize(size){
    buffer = (uint8_t*) malloc(size);
    cursor = 0;
}

CayenneLPP::~CayenneLPP(void){
    free(buffer);
}

void CayenneLPP::reset(void){
    cursor = 0;
}

//etorna o tamanho do buffer
uint8_t CayenneLPP::getSize(void){
    return cursor;
}

//Retorna um ponteiro para o buffer
uint8_t* CayenneLPP::getBuffer(void){
    return buffer;
}

//Copia o buffer interno para um buffer especificado e retorna o tamanho copiado
uint8_t CayenneLPP::copy(uint8_t* dst){
    memcpy(dst, buffer, cursor);
    return cursor;
}

uint8_t CayenneLPP::addLuminosity(uint8_t canal, uint16_t lux){
    if ((cursor + LPP_LUMINOSITY_SIZE) > maxsize) {
        return 0;
    }
    buffer[cursor++] = channel; 
    buffer[cursor++] = LPP_LUMINOSITY; 
    buffer[cursor++] = lux >> 8; 
    buffer[cursor++] = lux; 

    return cursor;
}

uint8_t CayenneLPP::addPresence(uint8_t channel, uint8_t value){
    if ((cursor + LPP_PRESENCE_SIZE) > maxsize) {
        return 0;
    }
    buffer[cursor++] = channel; 
    buffer[cursor++] = LPP_PRESENCE; 
    buffer[cursor++] = value; 

    return cursor;
}

uint8_t CayenneLPP::addTemperature(uint8_t ChannelTemp, float temp){
    if ((cursor + LPP_TEMPERATURE_SIZE) > maxsize) {
        return 0;
    }
    int16_t val = temp * 10;
    buffer[cursor++] = ChannelTemp; 
    buffer[cursor++] = LPP_TEMPERATURE; 
    buffer[cursor++] = val >> 8; 
    buffer[cursor++] = val; 

    return cursor;
}

uint8_t CayenneLPP::addRelativeHumidity(uint8_t ChannelUmid, float umid){
    if ((cursor + LPP_RELATIVE_HUMIDITY_SIZE) > maxsize) {
        return 0;
    }
    buffer[cursor++] = ChannelUmid; 
    buffer[cursor++] = LPP_RELATIVE_HUMIDITY; 
    buffer[cursor++] = umid * 2; 

    return cursor;
}

uint8_t CayenneLPP::addBarometricPressure(uint8_t ChannelPress, float pres){
    if ((cursor + LPP_BAROMETRIC_PRESSURE_SIZE) > maxsize) {
        return 0;
    }
    int16_t val = pres / 100;
    
    buffer[cursor++] = ChannelPress; 
    buffer[cursor++] = LPP_BAROMETRIC_PRESSURE; 
    buffer[cursor++] = val >> 8; 
    buffer[cursor++] = val; 

    return cursor;
}
uint8_t CayenneLPP::addAccelerometer(uint8_t channel, float x, float y, float z){
    if ((cursor + LPP_ACCELEROMETER_SIZE) > maxsize) {
        return 0;
    }
    int16_t vx = x * 1000;
    int16_t vy = y * 1000;
    int16_t vz = z * 1000;
    
    buffer[cursor++] = channel; 
    buffer[cursor++] = LPP_ACCELEROMETER; 
    buffer[cursor++] = vx >> 8; 
    buffer[cursor++] = vx; 
    buffer[cursor++] = vy >> 8; 
    buffer[cursor++] = vy; 
    buffer[cursor++] = vz >> 8; 
    buffer[cursor++] = vz; 

    return cursor;
}

uint8_t CayenneLPP::addGyrometer(uint8_t canal, float x, float y, float z){
    if ((cursor + LPP_GYROMETER_SIZE) > maxsize) {
        return 0;
    }
    int16_t vx = x * 100;
    int16_t vy = y * 100;
    int16_t vz = z * 100;
    
    buffer[cursor++] = channel; 
    buffer[cursor++] = LPP_GYROMETER; 
    buffer[cursor++] = vx >> 8; 
    buffer[cursor++] = vx; 
    buffer[cursor++] = vy >> 8; 
    buffer[cursor++] = vy; 
    buffer[cursor++] = vz >> 8; 
    buffer[cursor++] = vz; 

    return cursor;
}

uint8_t CayenneLPP::addGPS (canal de uint8_t, latitude de flutuador, longitude flutuante, medidores de flutuação){
    if ((cursor + LPP_GPS_SIZE) > maxsize) {
        return 0;
    }
    int32_t lat = latitude * 10000;
    int32_t lon = longitude * 10000;
    int32_t alt = meters * 100;
    
    buffer[cursor++] = channel; 
    buffer[cursor++] = LPP_GPS; 

    buffer[cursor++] = lat >> 16; 
    buffer[cursor++] = lat >> 8; 
    buffer[cursor++] = lat; 
    buffer[cursor++] = lon >> 16; 
    buffer[cursor++] = lon >> 8; 
    buffer[cursor++] = lon; 
    buffer[cursor++] = alt >> 16; 
    buffer[cursor++] = alt >> 8;
    buffer[cursor++] = alt;

    return cursor;
}
