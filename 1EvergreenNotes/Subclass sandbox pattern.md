# Subclass sandbox pattern
https://gameprogrammingpatterns.com/subclass-sandbox.html?utm_source=pocket_mylist

add protected methods in a base class for each atomic "query" to different subsystems. Useful when programming subclasses that will use many different subclasses. Any of these protected methods are used in a virtual Activate() method. 

Here is another good reason to use inheritance - to restrict usage of some methods.

```
class Superpower
{
public:
  virtual ~Superpower() {}

protected:
  virtual void activate() = 0;

  void move(double x, double y, double z)
  {
    // Code here...
  }

  void playSound(SoundId sound, double volume)
  {
    // Code here...
  }

  void spawnParticles(ParticleType type, int count)
  {
    // Code here...
  }
};
```
```
class SkyLaunch : public Superpower
{
protected:
  virtual void activate()
  {
    // Spring into the air.
    playSound(SOUND_SPROING, 1.0f);
    spawnParticles(PARTICLE_DUST, 10);
    move(0, 0, 20);
  }
};
```




---
status: #🌾
tags: #gamedev/patterns 
related: 