# ami_ass
Assignment 2 1702



int blur(char * radius, char * input, char * output){
    int y = 0, x = 0, colour;

    int rad = atoi(radius);
    Bmp img = read_bmp(input);
    Bmp copy_img = copy_bmp(img);


    while(y < img.height){
        while (x < img.width){
            for(colour = 0; colour < 3; colour++){

                int area = pow((2*rad+1), 2);
                int sum = 0;
                int lat = -rad, lon = -rad; //Inspired by longditude and latitude
                while (lon < rad+1){
                    lat = -rad;
                    if (y+lon < 0 || y+lon > img.height-1){
                        area -= (2*rad+1);
                        lon += 1;
                        continue;
                    }

                    while (lat < rad+1){
                        if (x + lat < 0 || x+lat > img.width-1){
                            area -=1;
                            lat += 1;
                            continue;
                        }
                        else{
                            sum += (img.pixels[y+lon][x+lat][colour]);
                            lat += 1;
                        }
                    }
                    lon += 1;
                }
                int av = 0;
                if (area > 0) (av = sum/area);
                copy_img.pixels[y][x][colour] = av;
            }
            // }
            x +=1;
        }
        y += 1;
        x = 0;
    }
    write_bmp(copy_img, output);
    free_bmp(img);

    return(0);
}
