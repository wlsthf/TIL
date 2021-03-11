## spring_ redirect

```java
ModelAndView mav = new ModelAndView();
//mav.setView(new RedirectView("/abc/def/ghi.do?param=1"));
mav.setViewName("/abc/def/ghi.do?param=1");
// mav.addObject("error", 500);
return mav;
```

