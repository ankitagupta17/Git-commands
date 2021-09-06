# Git-commands

git checkout -b feature/HOMEAAMI-966
(switch to new branch)

git status

git add -A

git status
(changes to be committed)

git commit -m "[ANKITA] HOMEAAMI-966"

git push origin feature/HOMEAAMI-966


TO RUN TEST CASES

npm install jest -global

jest

jest classname

npm run jest

npm run jest -- -u

npm run jest filename



to pull the code from feature branch
open git bash
go to the folder 
git pull origin feature/HOMENB-875
to make a new branch
git checkout feature/HOMENB-875




# Code deploy
1. Commit the code
2. Open jenkins. Jenkins has 2 pipelines: build and deploy
    build: /job/DIS-Projects/job/home/job/DIS-homeonline-nb-pipeline/   (mvn clean install & build.bat)
    deploy: /job/DIS-Projects/job/home/job/DIS-homeonline-deployment
3. follow the steps from videos
4. while building, as we are not pushing the code and just checking if it will work on UAT environment or not.
   select "skip" in the dropdown when it asks for the input from the user(a --- boundary is created)
5. If it is successful. Copy the artifact id from the build console, paste it on the box in the deploy url -> build with parameters. clcik on the build and check the build.
6. After it is done, check all the changes in the test url. 

artifact --> war file which is generated
environment --> develop, test, uat





# cmd commands, to check which ports are up and to stop them.
netstat -ano | findstr 9000                                 //9000 is port number
taskkill /F /PID 34924                                     //34929 is pID



JAVA STUFF

composite key,
controller advice,
bad request,
junit 5,
@propertysource
profiles mocking
spring security



spring profiles active



to get the message:
use @ContollerAdvice for generic Exception

@org.springframework.web.bind.annotation.ControllerAdvice
@RestController
public class ControllerAdvice extends ResponseEntityExceptionHandler {

    @ExceptionHandler(GenericException.class)
    public ResponseEntity<Object> handleException(
            GenericException ex, WebRequest request)
    {
        Map<String,Object> map=new LinkedHashMap<>();
        map.put("message",ex.getMessage());
        return new ResponseEntity<>(map, HttpStatus.BAD_REQUEST);
    }
}


public class GenericException extends RuntimeException{
    public GenericException(String message)
    {
        super(message);
    }
}


@PostMapping("/addItems")
    public ResponseEntity<String> addItems(@Validated @RequestBody ItemModel items, BindingResult bindingResult) {
        if(!bindingResult.hasErrors()) {
            try {
                itemService.addItems(items);
            }
            catch (Exception e){
                throw new GenericException(e.getMessage());
            }
        } else {
            return new ResponseEntity<String>("Field Required", HttpStatus.BAD_REQUEST);
        }
        return new ResponseEntity<String>("Item SuccessFully Added", HttpStatus.OK);
    }




Profiles in Spring:
1. open Run/debug configuration.
2. click on + -> maven -> 
	command line->  spring-boot:run 
	profiles->      

Runner --> untick project settings
VMOptions-> -Dspring.profiles.active=dev

Apply

3. In controller class, add

 @Value("${message}")
    private String message;

after @Autowired annotation.


    @PostMapping("/addCategory")
    public ResponseEntity<String> addCategory(@Validated @RequestBody CategoryModel category, BindingResult bindingResult) {
        System.out.println("aa "+message);

4. aaplication.properties

spring.profiles.active=dev
message:"local envii"


