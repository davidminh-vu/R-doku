## Scales of Measure
![image](https://user-images.githubusercontent.com/25742415/196103314-00a41e51-c6dd-4ca1-a771-fe464ffc6281.png)

## Datatypes
![grafik](https://user-images.githubusercontent.com/25742415/208246240-e19c12ed-525e-43ef-93d3-c396758900db.png)

## Basic Dataset Methods
![grafik](https://user-images.githubusercontent.com/25742415/208249310-0aee88cb-de3d-4738-89f4-ab3f5d5fa1de.png)

### Subsetting
![grafik](https://user-images.githubusercontent.com/25742415/208249371-173b0b53-705f-4640-b5c7-cbbdbdffd7ac.png)

### Saving data
![grafik](https://user-images.githubusercontent.com/25742415/208249434-609e7812-9aa1-47b7-af5b-79320a370bf9.png)

### Graph types
![grafik](https://user-images.githubusercontent.com/25742415/208249468-ccdda1bc-9cd9-4bd5-ae4f-a0d46f397708.png)

## Tests
### Overview
![grafik](https://user-images.githubusercontent.com/25742415/208253680-922c3f6c-f4be-4602-8e77-42e5ab582555.png)

### Chi^2 Test
![grafik](https://user-images.githubusercontent.com/25742415/208253697-c214c7b3-e4c6-482e-a110-7bfcde304205.png)

#### Chi Test of approximation
![grafik](https://user-images.githubusercontent.com/25742415/208253744-d0466350-a83c-4f2b-865b-43e1ad3ad042.png)

```R
# See expected proportions
chisq.test(table(rfm_clean$Satisfaction),p=rep(1/2,2))$expected

# Actual test
chisq.test(table(rfm_clean$Satisfaction),p=rep(1/2,2))
```
![grafik](https://user-images.githubusercontent.com/25742415/208253809-3052a4e3-2559-4eb5-b110-5e1583ad98ce.png)

## Summary

