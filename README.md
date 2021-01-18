1. Determnien the number of training cells and the number of guard cells.
   Tr = 12 
   Td = 6 
   Gr= 6 
   Gd =3
2. Select the offset as 6DB.
3. Select the grid that includes the training, guard and test cells. Grid Size = (2Tr+2Gr+1)(2Td+2Gd+1).
4.The total number of cells in the guard region and cell under test. (2Gr+1)(2Gd+1).
6.his gives the Training Cells : (2Tr+2Gr+1)(2Td+2Gd+1) - (2Gr+1)(2Gd+1)
7.Slide the Cell Under Test (CUT) across the complete cell matrix. For each iteration, measure and average the noise across all the training cells. This gives the threshold.
  for i = 1:(Nr/2 - (2*Gr+2*Tr))
    for j = 1:(Nd - (2*Gd+2*Td))
        % Now for each step, add the noise within all the training cells   
        % Taking the leading cell average here
        s1 = sum(db2pow(RDM(i:i+2*Tr+2*Gr, j:j+2*Td+2*Gd)),'all');
        s2 = sum(db2pow(RDM(i+Tr:i+Tr+2*Gr, j+Td:j+Td+2*Gd)),'all');    
        noise_level = s1 - s2;       
        
        threshold = noise_level/num_cells;  
8. Add the offset (if in signal strength in dB) to the threshold to keep the false alarm to the minimum.convert the value from logarithmic to linear using db2pow function.
        threshold = db2pow(pow2db(threshold)+offset);
9.Determine the signal level at the Cell Under Test. If the CUT signal level is greater than the Threshold, assign a value of 1, else equate it to zero. 
    
       
