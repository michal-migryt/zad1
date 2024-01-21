# zad1

Utworzenie namespace'a - namespace.yaml
<br>
![image](https://github.com/michal-migryt/zad1/assets/65659701/85f9b0bc-127b-4bac-9e98-b548439073d2)
<br>
1. Ograniczenia zasobów dla ns zad5 - resource-quota.yaml
<br>
![image](https://github.com/michal-migryt/zad1/assets/65659701/83b2337c-86ba-42bf-ba46-aacd6a704251)
<br>
2. Utworzenie manifestu pod worker - worker.yaml
<br>
![image](https://github.com/michal-migryt/zad1/assets/65659701/b5564955-e4bb-44b2-9465-b88a52a64631)
<br>
3. Przerobiony php-apache.yaml
<br>
![image](https://github.com/michal-migryt/zad1/assets/65659701/2dfe89f7-e639-47ea-ac3a-6748e636173e)
<br>
4. Definicja HorizontalPodAutoscaler'a - horizontal-autoscaler.yaml
<br>
Maxreplicas zostało ustawione na 5, tak aby w przypadku maksymalnego obciazenia wszystkich podow, a wiec 5 podow apache oraz poda worker, nie przekroczyc ustawionej w resources-quota 1.5Gi pamieci RAM.
<br>
![image](https://github.com/michal-migryt/zad1/assets/65659701/55a33b13-6c30-4f77-96e4-76a402986de0)
<br>
5. Utworzenie obiektów
<br>
![image](https://github.com/michal-migryt/zad1/assets/65659701/2c8b146d-4f52-4cfc-b7f7-805ea8143e63)
<br>
Potwierdzenie uruchomienia:
<br>
![image](https://github.com/michal-migryt/zad1/assets/65659701/286712ed-ca4d-42da-92c7-465a96c634d6)
<br>
6. Obciążenie i test autoskalowania wykonany przy użyciu zmodyfikowanego polecenia z https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/ :
<br>
kubectl run -i --tty load-generator2 --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://php-apache.zad5; done"
<br>
Efekt po obciążeniu:
<br>
![image](https://github.com/michal-migryt/zad1/assets/65659701/e4ebea0f-c766-4075-ac4e-6639292f8807)
<br>
Używane zasoby:
<br>
![image](https://github.com/michal-migryt/zad1/assets/65659701/47934f8b-3de2-4767-95d9-4261dc140a8e)
<br>
Jak widać pozostaje wolne 686 Mi RAM'u do użycia, które w przypadku zwiększonego obciazenia RAM wszystkich podow zmalałoby do 86 RAM, więc wykorzystywany jest bezpiecznie potencjał zasobów.
