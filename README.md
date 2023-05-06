int dataa (char * data) {

    char d;
    int i;
    i=0;
    d = UART_Read();
    while(d != '$') {
        d = UART_Read();
    }

    while (d != '*'){
        data[i]= d;
        d = UART_Read();
        i = i+1;
    }
    if(data[1] == 'G' && data[2] == 'P' && data[3] == 'G' && data[4] == 'G' && data[5] == 'A') {
        return i+1;
    }
    else {
        return -1;
    }
}


uint32_t  parsing (char * Gpsdata, char * latitude, char * longitude, int size)
{	int lat_start, lat_end, lon_start ,lon_end;
    uint32_t i;
		uint32_t j;
		uint32_t k;
		uint32_t a;
		uint32_t b;
		uint32_t flag1;
	uint32_t flag2;
	uint32_t counter;
	flag1=0;
	flag2=0;
	counter=0;
    
    for(i = 0; i<size; i++) {
			
        if(Gpsdata[i] == ',') {
            counter++;
            if(counter == 2) {
                lat_start = i+1;
            }
            if(counter == 3) {
                lat_end = i-1;
            }
            if(counter == 4) {
                lon_start = i+1;
            }
            if(counter == 5) {
                lon_end = i-1;
							
            }
        }
    }
    a = 0;
    for(j=lat_start; j<=lat_end; j++) {
        latitude[a] =(char) (Gpsdata[j]);
        a++;
			flag1=1;
    }
    b = 0;
    for(k=lon_start; k<=lon_end; k++) {
        longitude[b] = (char)(Gpsdata[k]);
        b++;
			flag2=1;
    }
		
		 
		if(flag1&&flag2)
				return 1;
		else
		    return 0;
}


void swap(char * LA1, char * LO1, char * LA2, char * LO2)
{
	uint8_t i;
	for( i=0; i<9; i++)
	{
		LA1[i] = LA2[i];
	}
	for(i=0; i<10; i++)
	{
		LO1[i] = LO2[i];
	}
}
