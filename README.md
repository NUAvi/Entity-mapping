# Entity-mapping

package City.example.City.Model;

import lombok.*;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.Table;
import java.util.Date;
@Entity
@AllArgsConstructor
@NoArgsConstructor
@Getter
@Setter
@Data
@Table(name="film_actor")
public class FilmActor {
    @Id
    @GeneratedValue
    private Integer ActorId;
    private Integer FilmId;
    private Date LastUpdte;
}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
package City.example.City.Repository;

import City.example.City.Model.FilmActor;
import org.springframework.data.jpa.repository.JpaRepository;

public interface FilmActorRepository extends JpaRepository<FilmActor,Integer> {
}
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
package City.example.City.Service;
import City.example.City.Model.FilmActor;
import City.example.City.Repository.FilmActorRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class FilmActorService {
    @Autowired
    private FilmActorRepository filmActorRepository;



    public List<FilmActor> getAllFilmActors() {

        return filmActorRepository.findAll();
    }
    public void addFilmActor(FilmActor filmActor)
    {
        filmActorRepository.save(filmActor);
    }
}
-----------------------------------------------------------------------------------------------------------------------------------------------------------------
package City.example.City.Controler;
import City.example.City.Model.FilmActor;
import City.example.City.Service.FilmActorService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
public class FilmActorControler {
    @Autowired
    private FilmActorService filmactorService;
    @GetMapping("/filmActor")
    public List<FilmActor> getAllFilmActors()
    {
        return filmactorService.getAllFilmActors();
    }
    @RequestMapping(value="/filmActor1", method= RequestMethod.POST)
    public void addFilmActor(@RequestBody FilmActor userRecord)
    {
        filmactorService.addFilmActor(userRecord);
    }
}
