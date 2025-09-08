1. Investigate the source table definiton what you want to make etl 
2. Create Table on Vertica DB (Data warehouse)
3. Create Table Definition on Source and Target
   
<img width="665" height="483" alt="image" src="https://github.com/user-attachments/assets/f97ce879-964d-44fb-a5fa-1ba12d038a83" />

4. Create JOB on IBM DataStage
   2-1 Copy existing job
   2-2 Rename copied job and change the table on source, target
   2-3 Create new table definiton if there was no definition already
5. Run to test ( Do not run in no-changed table name )

   
