---
layout: post
title: "Springboot junit service unit test with pageable jpa repository"
categories: bashscript
---

Below is an example how to test pagination of collections with `Pageable` by Spring Data JPA 

```
@Test
    public void showAllBrands() {
        int pageNumber = 0;
        int pageSize = 1;

        Pageable pageable = PageRequest.of(pageNumber, pageSize);

        Brand brand = convertToEntity(brandRequestDTO());

        Page<Brand> brandsPage = new PageImpl<>(Collections.singletonList(brand));

        when(brandRepository.findAll(pageable))
                .thenReturn(brandsPage);

        List<BrandResponseDTO> brandResponseDTOS = brandsPage.stream()
                .map(brandPage -> modelMapper.map(brand, BrandResponseDTO.class))
                .collect(Collectors.toList());

        PaginateBaseResponseDTO<HttpStatus, String, List<BrandResponseDTO>> expected = new PaginateBaseResponseDTO<>(
                HttpStatus.OK,
                "successfully retrieving data",
                brandResponseDTOS,
                1L,
                1,
                1
        );

        PaginateBaseResponseDTO<HttpStatus, String, List<BrandResponseDTO>> actual = brandService.listAllBrands(pageable);

        assertThat(actual).usingRecursiveComparison().isEqualTo(expected);
    }
```

Nice to read https://keepgrowing.in/java/springboot/add-pagination-to-a-spring-boot-app/