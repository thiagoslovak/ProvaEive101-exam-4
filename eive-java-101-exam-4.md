# Prova Modulo 4

## Docker / Postgres

  - Faça o clone do projeto `https://github.com/spring-projects/spring-petclinic.git`.
  - Crie o `dockerfile` necessário para a construção e execução do projeto, considere que o projeto utilizará o `spring.profiles.active` de postgres.
  - Configure o projeto para que a pasta `target` seja ignorada pelo docker ao construir a imagem.
  - Construa o projeto utilizando a seguinte tag: `eive-java-exam-4:prod`.
  - Suba a imagem para o docker hub e vincule a URL da imagem na atividade.
  - Vincule o comando necessário para rodar o container da imagem criada considerando que ela será baixada do docker hub e conectará no postgres.
    - Atenção: as credenciais de acesso ao banco devem ser informadas através de variáveis de ambiente.



  - URL: https://hub.docker.com/repository/docker/thiagoslovak/eive-java-exam-4

  - Comando para rodar:

    - ````
        docker run -p 8080:8080 thiagoslovak/eive-java-exam-4:prod
        ````

        

  - Dockerfile:

    - ````dockerfile
        FROM openjdk
        
        RUN mkdir -p /app/eive-java-101-exam-4
        
        ENV APP_NAME=spring-petclinic.jar
        
        ENV POSTGRES_URL=jdbc:postgresql://postgres:5432/petclinic
        				 
        ENV POSTGRES_USER=petclinic
        
        ENV POSTGRES_PASS=petclinic
        
        COPY ${APP_NAME} /app/eive-java-101-exam-4
        
        EXPOSE 8080
        
        ENTRYPOINT [ "java", "-Dspring.profiles.active=postgres", "-jar", "/app/eive-java-101-exam-4/spring-petclinic.jar" ]
        
        ````

        

    

## MongoDB

  - Faça o clone do respositório `https://github.com/mcampo2/mongodb-sample-databases.git`.

  - Importe o `dataset` localizado em `sample_airbnb` (mongoimport - MongoDB Database Tools).

    - ````
      mongoimport --db exam --collection airbnb --type json --file listingsAndReviews.json
      ````

  - Realize as seguintes operações (utilizar `mongosh` e vincular as _queries_ executadas):
    - Inserir um novo registro de imóvel para aluguel conforme estrutura já existente.

      - ````
        db.airbnb.insertOne(
        {
          _id: '24',
          listing_url: 'https://www.airbnb.com/rooms/10021707',
          name: 'Private Room in Bushwick',
          summary: 'Here exists a very cozy room for rent in a shared 4-bedroom apartment. It is located one block off of the JMZ at Myrtle Broadway.  The neighborhood is diverse and appeals to a variety of people.',
          space: '',
          description: 'Here exists a very cozy room for rent in a shared 4-bedroom apartment. It is located one block off of the JMZ at Myrtle Broadway.  The neighborhood is diverse and appeals to a variety of people.',
          neighborhood_overview: '',
          notes: '',
          transit: '',
          access: '',
          interaction: '',
          house_rules: '',
          property_type: 'Apartment',
          room_type: 'Private room',
          bed_type: 'Real Bed',
          minimum_nights: '14',
          maximum_nights: '1125',
          cancellation_policy: 'flexible',
          last_scraped: ISODate("2019-03-06T05:00:00.000Z"),
          calendar_last_scraped: ISODate("2019-03-06T05:00:00.000Z"),
          first_review: ISODate("2016-01-31T05:00:00.000Z"),
          last_review: ISODate("2016-01-31T05:00:00.000Z"),
          accommodates: 1,
          bedrooms: 1,
          beds: 1,
          number_of_reviews: 1,
          bathrooms: Decimal128("1.5"),
          amenities: [
            'Internet',
            'Wifi',
            'Air conditioning',
            'Kitchen',
            'Buzzer/wireless intercom',
            'Heating',
            'Smoke detector',
            'Carbon monoxide detector',
            'Essentials',
            'Lock on bedroom door'
          ],
          price: Decimal128("40.00"),
          extra_people: Decimal128("0.00"),
          guests_included: Decimal128("1"),
          images: {
            thumbnail_url: '',
            medium_url: '',
            picture_url: 'https://a0.muscache.com/im/pictures/72844c8c-fec2-440e-a752-bba9b268c361.jpg?aki_policy=large',
            xl_picture_url: ''
          },
          host: {
            host_id: '11275734',
            host_url: 'https://www.airbnb.com/users/show/11275734',
            host_name: 'Josh',
            host_location: 'New York, New York, United States',
            host_about: '',
            host_thumbnail_url: 'https://a0.muscache.com/im/users/11275734/profile_pic/1405792127/original.jpg?aki_policy=profile_small',
            host_picture_url: 'https://a0.muscache.com/im/users/11275734/profile_pic/1405792127/original.jpg?aki_policy=profile_x_medium',
            host_neighbourhood: 'Bushwick',
            host_is_superhost: false,
            host_has_profile_pic: true,
            host_identity_verified: true,
            host_listings_count: 1,
            host_total_listings_count: 1,
            host_verifications: [ 'email', 'phone', 'reviews', 'kba' ]
          },
          address: {
            street: 'Brooklyn, NY, United States',
            suburb: 'Brooklyn',
            government_area: 'Bushwick',
            market: 'New York',
            country: 'United States',
            country_code: 'US',
            location: {
              type: 'Point',
              coordinates: [ -73.93615, 40.69791 ],
              is_location_exact: true
            }
          },
          availability: {
            availability_30: 0,
            availability_60: 0,
            availability_90: 0,
            availability_365: 0
          },
          review_scores: {
            review_scores_accuracy: 10,
            review_scores_cleanliness: 10,
            review_scores_checkin: 10,
            review_scores_communication: 10,
            review_scores_location: 8,
            review_scores_value: 8,
            review_scores_rating: 100
          },
          reviews: [
            {
              _id: '61050713',
              date: ISODate("2016-01-31T05:00:00.000Z"),
              listing_id: '10021707',
              reviewer_id: '52006105',
              reviewer_name: 'Antoine',
              comments: "Josh was out of town during my 1 month stay. His roommates greeted and helped get me settled. They were great hosts and all around cool people. I'm a Brooklynite, but have never lived in Bushwick.\r\n" +
                "If you're looking for an hip, authentic, and convenient Brooklyn experience, this spot is for you.  You can literally see the Subway platform from Josh's window. Also a couple steps away from anything you could possibly need... restaurants, juice bar, organic grocery, etc. "
            }
          ]
        })	
        ````

    - Alterar o valor do preço diário (`price`) para `500` do registro incluído.

      - ````
        db.airbnb.updateOne({ _id:'24' }, { $set: { price: Decimal128("500.00") } } )
        ````

    - Informar apenas o valor do apartamento com diária (`price`)  mais cara disponível no Brasil (`BR`) sem retornar o campo `_id`.

      - ````
        db.airbnb.find({"address.country_code":'BR'}, {_id:0}).sort({price:-1}).limit(1)
        ````
