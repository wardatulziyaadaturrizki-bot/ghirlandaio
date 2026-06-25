```
mkdir nova                          
cd nova/
```
```                                                                                                                                      
mkdir omeka                                                                                                                                            
cd omeka/    
```
```
mkdir config                                                                                                                                          
mkdir files                                                                                                                                           
ls                                                                                                                                                    
config  files  
```
```
chmod -R 777 /config                                                                                                                                                         
chmod -R 777 config/                                                                                                                                  
chmod -R 777 files/
```
```                                                                                                                       
ls -la                                                                                                                                                                                                                                                                                    
cd config/                                                                                                                                            
ls                                                                                                                                                   
nvim database.ini
```

<img width="71" height="34" alt="Screenshot 2026-06-25 202346" src="https://github.com/user-attachments/assets/4ed1c874-067e-4fa0-9ffd-cd19c6117acc" />

```
cd ..                                                                                                                                                
nvim docker-compose.yml
```

<img width="193" height="106" alt="Screenshot 2026-06-25 203603" src="https://github.com/user-attachments/assets/f81de28c-5316-4884-bc28-e1d7188ab6a5" />

```
podman compose up -d                                                                                                                                  
ls                                                                                                                                                    
nvim docker-compose.yml  
```

<img width="203" height="128" alt="Screenshot 2026-06-25 203845" src="https://github.com/user-attachments/assets/5b310a19-97c4-4ea1-b642-a1505254fc91" />


