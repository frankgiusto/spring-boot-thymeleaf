# WET Centrally Distributed Template Solution (CDTS) for Spring Boot and Thymeleaf

This is a Spring Boot Starter that uses Thymeleaf to implement CDTS.

## Building wet-cdts-spring-boot-thymeleaf-starter

* Clone the repository
* From the repository root, run `maven install`

## How to use wet-cdts-spring-boot-thymeleaf-starter

1) Add the starter to your projects POM file.

    <dependency>
      <groupId>ca.canada.ised.wet.cdts</groupId>
      <artifactId>wet-cdts-spring-boot-thymeleaf-starter</artifactId>
      <version>4.0.21.4</version>
    </dependency>

2) Add the WETTemplateInterceptor to your applications list of interceptors.


    /**
     * Web configuration.
     */
    @Configuration
    public class WebConfig extends WebMvcConfigurerAdapter {
    
        /** The cdn template interceptor. */
        @Autowired
        private WETTemplateInterceptor cdnTemplateInterceptor;
        
        /** {@inheritDoc} */
        @Override
        public void addInterceptors(InterceptorRegistry registry) {
            super.addInterceptors(registry);
            registry.addInterceptor(cdnTemplateInterceptor);
        }
    }

3) Use one of the supplied templates as the basis for your Thymeleaf templates.

    <html xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout" layout:decorator="layouts/layout">
      <head>
        <title>Page Title</title>
	   </head>
	   <body>		
        <div layout:fragment="content">
          <div>This content will be included in the "content" div of the template.</div>
          <div>Language: <span data-th-text="#{lang}">lang</span></div>
          <div>This screen, home.html, uses <b>layout:decorator="layouts/layout"</b></div>
          <div class="row">
            <div class="col-md-4">
              <div class="form-group">
                <form action="#" data-th-action="@{#{url.sideMenu}}" method="post">					        
                  <button class="btn btn-primary" name="sideMenuButton" type="submit">See Side Menu Page</button>      
                </form>
              </div>
            </div>
          </div>
        </div>      
      </body>
    </html>