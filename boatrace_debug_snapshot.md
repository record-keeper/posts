# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-04-15T14:40:01.630196+09:00

### 次に取るべきアクション
> RED最優先: CRITICAL_ODDS_COLLAPSE×2 (24h) → ログ/DB確認

### 検出された問題
- 🟡 LARGE_ODDS_DRIFT×8 (24h)
- 🔴 CRITICAL_ODDS_COLLAPSE×2 (24h)

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🟡 HEALTH_CHECK_FAIL  ×2  [2026-04-15T14:00:02]
- key: `HEALTH_CHECK_FAIL`
- **FIX**: health.py の check 失敗→対応する check 名から該当テーブル/指標を確認

### ℹ️ ROI_STAT  ×1  [2026-04-15T13:53:08]
- key: `ROI_STAT|S11: n=32 hit%=0.0% hit_CI[Bonf]=[0.0,20.7]% ROI=0.00 ROI_boot95=[0.00,0.00]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-04-15T13:53:08]
- key: `INSUFFICIENT_SAMPLE|S11: n=32<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-04-15T13:53:08]
- key: `ORPHAN_SCAN|2 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ ROI_STAT  ×2  [2026-04-15T13:50:34]
- key: `ROI_STAT|S00: n=41 hit%=46.3% hit_CI[Bonf]=[26.5,67.5]% ROI=0.97 ROI_boot95=[0.62,1.41]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×2  [2026-04-15T13:50:34]
- key: `ROI_STAT|S02: n=134 hit%=10.4% hit_CI[Bonf]=[5.0,20.5]% ROI=0.23 ROI_boot95=[0.14,0.54]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×2  [2026-04-15T13:50:34]
- key: `ROI_STAT|S03: n=74 hit%=16.2% hit_CI[Bonf]=[7.4,31.9]% ROI=0.32 ROI_boot95=[0.19,0.76]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×2  [2026-04-15T13:50:34]
- key: `ROI_STAT|S07: n=43 hit%=39.5% hit_CI[Bonf]=[21.5,61.0]% ROI=0.81 ROI_boot95=[0.54,1.46]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×2  [2026-04-15T13:50:34]
- key: `ROI_STAT|S09: n=41 hit%=46.3% hit_CI[Bonf]=[26.5,67.5]% ROI=0.97 ROI_boot95=[0.62,1.41]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### 🟡 ORPHAN_SCAN  ×1  [2026-04-15T13:50:34]
- key: `ORPHAN_SCAN|9 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-04-15T13:50:33]
- key: `PAYOUT_RATIO_WEIRD|pid=418 bet=200 odds=5.6 payout=260 ratio=0.23`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-04-15T13:50:33]
- key: `PAYOUT_RATIO_WEIRD|pid=490 bet=300 odds=6.9 payout=420 ratio=0.20`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-04-15T13:50:33]
- key: `PAYOUT_RATIO_WEIRD|pid=508 bet=300 odds=8.1 payout=450 ratio=0.19`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-04-15T13:50:33]
- key: `PAYOUT_RATIO_WEIRD|pid=556 bet=100 odds=6.7 payout=130 ratio=0.19`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-04-15T13:50:33]
- key: `PAYOUT_RATIO_WEIRD|pid=578 bet=500 odds=13.1 payout=1350 ratio=0.21`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-04-15T13:50:33]
- key: `PAYOUT_RATIO_WEIRD|pid=595 bet=300 odds=8.2 payout=570 ratio=0.23`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-04-15T13:50:33]
- key: `PAYOUT_RATIO_WEIRD|pid=638 bet=500 odds=11.2 payout=1600 ratio=0.29`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-04-15T13:50:33]
- key: `PAYOUT_RATIO_WEIRD|pid=670 bet=500 odds=10.2 payout=500 ratio=0.10`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-04-15T13:50:33]
- key: `PAYOUT_RATIO_WEIRD|pid=688 bet=500 odds=9.0 payout=500 ratio=0.11`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視

### 🟡 PAYOUT_RATIO_WEIRD  ×2  [2026-04-15T13:50:33]
- key: `PAYOUT_RATIO_WEIRD|pid=530 bet=100 odds=26.0 payout=210 ratio=0.08`
- **FIX**: 同着分割 or 直前オッズ崩落の実現象。CRITICAL ではない、件数のみ監視


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `1193885b4bcdeb4c8d16955d7ee412db`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 0.99MB / last modified 2026-04-15T14:39:34.637377+09:00

### データファイル存在確認
| file | exists | md5 | size |
|---|---|---|---|
| lgbm_model_top1.txt | True | `5b55d55bdb59df95ccfd1745d4e9b469` | 769682 |
| lgbm_model_top3.txt | True | `d5fd8d8393fd859ed913813abbf60084` | 969111 |
| calibration_v7.json | True | `1c04ab3c1a1f074da889e6f5f06adbf3` | 1450 |
| pl_corr_v8_final.json | True | `8727224dfcc3d7548845e2e41caef7be` | 1209 |

### crontab
```
# boatrace_v2 - managed by めう/Claude
SHELL=/bin/bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# 1分毎: 統合サイクル (run_cycle.py, flock で並行実行防止)
* 8-23 * * * cd /opt/boatrace_v2 && flock -n /var/lock/run_cycle.lock /opt/boatrace/venv/bin/python3 run_cycle.py >> logs/run_cycle.log 2>&1

# 10分毎: pending alert flush
*/10 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 dispatch_pending.py >> logs/dispatch.log 2>&1

# 10分毎: snapshot 生成 + GitHub 同期 (Claude 次セッション用)
*/10 * * * * cd /opt/boatrace_v2 && bash sync_snapshot_to_github.sh >> logs/sync_snapshot.log 2>&1

# 5分毎: 結果取得
*/5 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 record_results.py >> logs/results.log 2>&1

# 30分毎: health check
*/30 * * * * cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 health.py >> logs/health.log 2>&1

# 6時: 日次総合検査
0 6 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 verify_all.py >> logs/verify_all.log 2>&1

# 0時: 日次集計
5 0 * * *  cd /opt/boatrace_v2 && /opt/boatrace/venv/bin/python3 daily_summary.py >> logs/daily.log 2>&1
0 3 * * * find /opt -maxdepth 1 -name "boatrace_v2.bak_*" -mtime +7 -exec rm -rf {} \; # backup cleanup
```

### 直近 run_cycle ログ (末尾)
```
 parsed
2026-04-15 14:39:31,333 [INFO] scraper: odds2f: 15/15 parsed
2026-04-15 14:39:32,472 [INFO] scraper: odds_win: 6/6 parsed
2026-04-15 14:39:32,472 [INFO] scraper: fetch_race 09/9: boats=6 odds=191/191
2026-04-15 14:39:32,485 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-15 14:39:32,485 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-15 14:39:32,493 [INFO] run_cycle: fetched 09/9 [final]: 156 combos
2026-04-15 14:39:32,499 [INFO] race_id: notif: nid=2026041509091442 sid=S01 phase=final rank=
2026-04-15 14:39:32,785 [INFO] notifier: Discord notify OK (status=204)
2026-04-15 14:39:33,227 [INFO] notifier: Discord notify OK (status=204)
2026-04-15 14:39:33,232 [INFO] run_cycle: RETREAT S01 津9R
2026-04-15 14:39:33,238 [INFO] race_id: notif: nid=2026041509091442 sid=S04 phase=final rank=
2026-04-15 14:39:33,624 [INFO] notifier: Discord notify OK (status=204)
2026-04-15 14:39:33,945 [INFO] notifier: Discord notify OK (status=204)
2026-04-15 14:39:33,998 [INFO] run_cycle: RETREAT S04 津9R
2026-04-15 14:39:34,008 [INFO] race_id: notif: nid=2026041509091442 sid=S06 phase=final rank=
2026-04-15 14:39:34,341 [INFO] notifier: Discord notify OK (status=204)
2026-04-15 14:39:34,633 [INFO] notifier: Discord notify OK (status=204)
2026-04-15 14:39:34,638 [INFO] run_cycle: RETREAT S06 津9R
2026-04-15 14:39:38,230 [INFO] scraper: odds3t: 120/120 parsed
2026-04-15 14:39:39,339 [INFO] scraper: odds3f: 20/20 parsed
2026-04-15 14:39:40,443 [INFO] scraper: odds2t: 30/30 parsed
2026-04-15 14:39:40,444 [INFO] scraper: odds2f: 13/15 parsed
2026-04-15 14:39:41,529 [INFO] scraper: odds_win: 6/6 parsed
2026-04-15 14:39:41,529 [INFO] scraper: fetch_race 03/9: boats=6 odds=189/191
2026-04-15 14:39:41,537 [INFO] predictor: CALIBRATION_MODE=shadow
2026-04-15 14:39:41,537 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-04-15 14:39:41,545 [INFO] run_cycle: fetched 03/9 [scan]: 156 combos
2026-04-15 14:39:41,644 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 2.5 | 0.55 | True |
| S01 | A | 2t | 5.0 | 0.6 | True |
| S02 | S | win | 5.0 | 0.1 | True |
| S03 | S | win | 5.0 | 0.2 | True |
| S04 | A | 2t | 5.0 | 0.55 | True |
| S05 | B | 3t | 10.0 | 0.4 | True |
| S06 | A | 2t | 5.0 | 0.5 | True |
| S07 | S | win | 3.0 | 0.5 | True |
| S08 | B | 3t | 10.0 | 0.5 | True |
| S09 | S | win | 2.5 | 0.55 | True |
| S10 | S | win | 2.25 | 0.6 | True |
| S11 | B | 3t | 10.0 | 0.2 | True |
| S12 | B | 3t | 10.0 | 0.4 | True |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 157
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 157
  }
]
```

## Phase別通知記録 (24h)
{'final': 80, 'scan': 77}

## アラート件数 (24h・種類別)
```
  LARGE_ODDS_DRIFT: 8
  CRITICAL_ODDS_COLLAPSE: 2
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 41 | 19 | 10,700 | 10,420 | -280 | 0.974 |
| S01 | 8 | 0 | 2,800 | 0 | -2,800 | 0.0 |
| S02 | 135 | 14 | 30,400 | 7,000 | -23,400 | 0.23 |
| S03 | 75 | 12 | 16,300 | 5,090 | -11,210 | 0.312 |
| S04 | 12 | 0 | 3,900 | 0 | -3,900 | 0.0 |
| S05 | 10 | 0 | 1,900 | 0 | -1,900 | 0.0 |
| S06 | 15 | 0 | 4,200 | 0 | -4,200 | 0.0 |
| S07 | 43 | 17 | 10,900 | 8,860 | -2,040 | 0.813 |
| S08 | 8 | 0 | 1,400 | 0 | -1,400 | 0.0 |
| S09 | 41 | 19 | 10,700 | 10,420 | -280 | 0.974 |
| S10 | 27 | 15 | 6,500 | 7,420 | +920 | 1.142 |
| S11 | 32 | 0 | 4,800 | 0 | -4,800 | 0.0 |
| S12 | 10 | 0 | 1,900 | 0 | -1,900 | 0.0 |

## 直近アラート (24h・新しい順)
```
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S12", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S12", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S11", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S11", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S08", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S08", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S05", "race": "174R", "combo": "1-6-5", "scan": 707.5, "final": 628.3, "drift_pct": -11.2}
[12:03:27] LARGE_ODDS_DRIFT: {"kind": "LARGE_ODDS_DRIFT", "sid": "S05", "race": "174R", "combo": "1-6-3", "scan": 501.1, "final": 672.6, "drift_pct": 34.2}
[11:03:29] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S03", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
[11:03:29] CRITICAL_ODDS_COLLAPSE: {"kind": "CRITICAL_ODDS_COLLAPSE", "sid": "S02", "race": "172R", "combo": "2", "scan": 72.7, "final": 25.7, "drift_pct": -64.6}
```

## 本日残レース: 62件

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S03 | 178R | win | 2 | 0.2118 | 31.8 | 6.73 | 300 | scan=30.0 drift=+6.0% | 14:04:24 |
| S02 | 178R | win | 2 | 0.2118 | 31.8 | 6.73 | 300 | scan=30.0 drift=+6.0% | 14:04:22 |
| S11 | 167R | 3t | 4-1-3 | 0.0357 | 312.5 | 11.17 | 100 | scan=- drift=- | 13:52:34 |
| S06 | 167R | 2t | 1-4 | 0.1341 | 66.9 | 8.97 | 200 | scan=71.5 drift=-6.4% | 13:52:33 |
| S04 | 167R | 2t | 1-4 | 0.1341 | 66.9 | 8.97 | 200 | scan=71.5 drift=-6.4% | 13:52:31 |
| S01 | 167R | 2t | 1-4 | 0.1341 | 66.9 | 8.97 | 200 | scan=71.5 drift=-6.4% | 13:52:30 |
| S06 | 176R | 2t | 1-5 | 0.1223 | 44.3 | 5.42 | 200 | scan=48.7 drift=-9.0% | 13:03:21 |
| S04 | 176R | 2t | 1-5 | 0.1223 | 44.3 | 5.42 | 200 | scan=48.7 drift=-9.0% | 13:03:20 |
| S03 | 164R | win | 3 | 0.1414 | 36.0 | 5.09 | 300 | scan=- drift=- | 12:27:21 |
| S02 | 164R | win | 3 | 0.1414 | 36.0 | 5.09 | 300 | scan=- drift=- | 12:27:20 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| 2t | 5 | -7.5% | -9.0% | -6.4% | 0 | 0 | 0 |
| 3t | 10 | +10.2% | -11.2% | +34.2% | 4 | 0 | 8 |
| win | 10 | -5.8% | -64.6% | +9.9% | 2 | 2 | 2 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

---
_auto-generated by claude_snapshot.py at 2026-04-15T14:40:01.630196+09:00_