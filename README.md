# Skapa EC2 med OpenTofu

## Meddelande från kunden

Vi behöver din hjälp! Vi har försökt sätta upp vår molninfrastruktur med OpenTofu, men något verkar vara fel. När vi kör våra skript får vi felmeddelanden och vi vet inte vad vi gör för fel.  

Vårt mål är att:  
- Skapa en EC2-instans i AWS  
- Definiera instanstyp och region  
- Använda en säkerhetsgrupp för att tillåta SSH-trafik  

Kan ni felsöka, hitta vad som är fel och få vår infrastruktur att fungera?  

Lycka till!  
**– Kundens DevOps Team**  

---

## Uppgift: Debugga och fixa infrastrukturen

1. Klona repo och navigera till projektmappen:
   ```bash
   git clone https://github.com/khdev-devops/infra-mar11-1-opentofu
   ```
   ```bash
   cd infra-mar11-1-opentofu
   ```

2. Installera OpenTofu i AWS CloudShell
   AWS CloudShell har redan nödvändiga AWS-behörigheter, så vi kan installera och köra OpenTofu direkt.

   Installera OpenTofu i CloudShell (behövs göras då och då eftersom CloudShell inte sparar installationer av paker och mjukvara):
   ```bash
   ./install_tofu.sh
   ```
   Kontrollera att OpenTofu är installerat:
   ```bash
   tofu --version
   ```

3. Skapa nycklar för att användas vid anslutaning till EC2 med SSH:
   ```bash
   ssh-keygen -t rsa -b 4096 -f ~/.ssh/tofu-key -N ""
   ```

4. Initiera och kör OpenTofu:
   ```bash
   tofu init
   tofu plan
   ```
   ❌ **Oj! Något är fel...**  
   Ni måste analysera felen och fixa konfigurationen!

5. Felsök och fixa problemen:
   - Läs felmeddelandena och försök förstå vad som saknas.
   - Titta igenom alla filer i repot för att se vad det innehåller och hitta ledtrådar.
   - Använd OpenTofu-dokumentationen (se nedan) för att hitta rätt syntax och lösningar

6. Testa om koden fungerar efter fixarna:
   ```bash
   tofu apply
   ```

7. Om EC2-instansen skapas korrekt ska ni:
   - se en IP-adress som output.
   - kunna göra ssh till den startade EC2-instansen, tex:
   ```bash
   ssh -i ~/.ssh/tofu-key ec2-user@<EC2-IP>
   ```
   Gick det? **Bra jobbat!** ✅

8. Ändra namnet på instansen och gör apply igen:
   - var kan du sätta namnet? Tänk ut minst två sätt.
   - kör `tofu apply` för att sjösätta ändringen.
   - titta i listan av EC2-instanser i AWS Console för att bekräfta att ändringen är utförd.

8. **Viktigt:** Städa upp efter dig genom att ta bort EC2-instansen:
   ```bash
   tofu destroy
   ```
   Notera att om du behöver denna EC2-instans igen kan du bara köra `tofu apply` igen.

---

## Hjälpmedel och resurser  

### Länkar
- [OpenTofu Dokumentation](https://opentofu.org/docs/)
- [Terraform .tfvars files: Variables Management with Examples](https://spacelift.io/blog/terraform-tfvars)
- [Variables & Outputs](https://opentofu.org/docs/language/values/)
- [Terraform AWS Provider](https://search.opentofu.org/provider/terraform-providers/aws/latest)
    - [Resource: EC2 instance](https://search.opentofu.org/provider/terraform-providers/aws/latest/docs/resources/instance)
- [State Files & Debugging](https://opentofu.org/docs/language/state/)