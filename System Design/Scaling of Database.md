
## Vertical Scaling

Advantages:
1. When the Load to your Database Increases then you would typically need more ram and more hardware resources
2. at that point what you will do is that you simply buy yourself more compute 
3. typically this is much easier (just a click away in cloud Providers)
4. This provides Downtime for some period because the data is being physically copied from one machine to another
Disadvantages:
1. This has an Upper Limit of Hardware Constraint which mean you can only scale up the hardware to only some extent you will reach your limit pretty soon.
## Horizontal Scaling

Read to write Ratio for a Normal Database is approximaly 90:10 Which means there is mostly reads than writes so what we do is that we make read Replica of that DataBase




