# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-06-01T15:20:01.408918+09:00

### 次に取るべきアクション
> RED最優先: CIRCUIT_BREAKER_TRIP×23 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×51 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×23 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×2 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×16  [2026-06-01T15:03:42]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×16  [2026-06-01T15:03:42]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-06-01T15:03:42]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×3  [2026-06-01T14:00:04]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×31  [2026-06-01T13:34:41]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×3  [2026-06-01T11:50:00]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_BET_VOLUME_DROP  ×7  [2026-06-01T09:00:39]
- key: `ANOMALY_BET_VOLUME_DROP|`
- **FIX**: 本日のbet数が7日baselineから2σ低下。戦略filter/ scan fix/run_cycle停止を疑え

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-01T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=9 pred=0.2241 actual=0.3333 gap=-0.1093`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-01T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-01T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-01T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S00: n=181<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-01T06:00:22]
- key: `DRIFT_BUCKET|drift ≥+30%: n=36 hit%=16.7% ROI=0.45 (コスト 9,200/回収 4,160)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-06-01T06:00:22]
- key: `CALIBRATION_LIVE|decile 0.10-0.15: n=6 pred=0.1265 actual=0.1667 gap=-0.0402`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-01T06:00:22]
- key: `ROI_STAT|S00: n=181 hit%=27.6% hit_CI[Bonf]=[19.2,38.0]% ROI=0.90 ROI_boot95=[0.66,1.17]`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ ROI_STAT  ×1  [2026-06-01T06:00:22]
- key: `ROI_STAT|S01_NAKAANA1: n=114 hit%=31.6% hit_CI[Bonf]=[20.6,45.0]% ROI=0.81 ROI_boot95=[0.`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-01T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S01_NAKAANA1: n=114<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### ℹ️ ROI_STAT  ×1  [2026-06-01T06:00:22]
- key: `ROI_STAT|S02_TETSUBAN: n=58 hit%=46.6% hit_CI[Bonf]=[29.3,64.7]% ROI=0.88 ROI_boot95=[0.6`
- **FIX**: 統計サマリ情報。判定ではなく参照用

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-06-01T06:00:22]
- key: `INSUFFICIENT_SAMPLE|S02_TETSUBAN: n=58<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-06-01T06:00:22]
- key: `ORPHAN_SCAN|230 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ DRIFT_BUCKET  ×1  [2026-06-01T06:00:22]
- key: `DRIFT_BUCKET|drift ≤-30%: n=49 hit%=30.6% ROI=0.87 (コスト 14,300/回収 12,480)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 4.01MB / last modified 2026-06-01T15:19:07.462624+09:00

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

# 30分毎: コード/DB a
```

### 直近 run_cycle ログ (末尾)
```
00, 'A': 6000, 'B': 1500} default=5000
2026-06-01 15:18:05,515 [INFO] predictor: Models loaded OK
2026-06-01 15:18:16,561 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=1&jcd=20&hd=20260601: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-01 15:18:27,644 [WARNING] scraper: fetch error (2/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=1&jcd=20&hd=20260601: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 3s
2026-06-01 15:18:40,697 [WARNING] scraper: fetch error (3/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=1&jcd=20&hd=20260601: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 9s
2026-06-01 15:18:40,697 [ERROR] scraper: fetch failed after 3 retries: https://www.boatrace.jp/owpc/pc/race/racelist?rno=1&jcd=20&hd=20260601
2026-06-01 15:18:40,697 [ERROR] scraper: racelist fetch failed: jcd=20 rno=1
2026-06-01 15:18:40,697 [WARNING] run_cycle: fetch None: 20/1
2026-06-01 15:18:51,935 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=1&jcd=01&hd=20260601: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-06-01 15:19:03,591 [INFO] scraper: odds3t: 120/120 parsed
2026-06-01 15:19:04,792 [INFO] scraper: odds3f: 20/20 parsed
2026-06-01 15:19:06,058 [INFO] scraper: odds2t: 30/30 parsed
2026-06-01 15:19:06,059 [INFO] scraper: odds2f: 14/15 parsed
2026-06-01 15:19:07,142 [INFO] scraper: odds_win: 4/6 parsed
2026-06-01 15:19:07,142 [INFO] scraper: fetch_race 01/1: boats=6 odds=188/191
2026-06-01 15:19:07,153 [INFO] predictor: CALIBRATION_MODE=on
2026-06-01 15:19:07,153 [INFO] predictor: combos: {'win': 4, '2t': 30, '3t': 120}
2026-06-01 15:19:07,161 [INFO] run_cycle: fetched 01/1 [scan]: 154 combos
2026-06-01 15:19:07,346 [INFO] run_cycle: run_cycle done: 0 notifications

```

## 戦略有効/無効一覧
| id | trust | bt | ev_th | pmin | enabled |
|---|---|---|---|---|---|
| S00 | S | win | 4.0 | 0.0 | True |
| S01_NAKAANA1 | A | win | 1.5 | 0.0 | True |
| S02_TETSUBAN | A | win | 1.0 | 0.0 | True |
| S03_NAKAANA4 | B | win | 1.0 | 0.0 | False |
| S04_SELL_3T | B | 3t | 1.0 | 0.0 | False |
| S05_2T_MANKEN | B | 2t | 1.0 | 0.0 | False |
| S06_2F_AXIS1 | B | 2f | 1.0 | 0.0 | False |
| S07_2T_HONMEI | B | 2t | 1.0 | 0.0 | False |

## Webhook送信 (24h)
```
[
  {
    "target": "mirror",
    "ok": 1,
    "c": 71
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 71
  }
]
```

## Phase別通知記録 (24h)
{'final': 28, 'result': 15, 'scan': 28}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 57
  FINAL_MISSING: 51
  CIRCUIT_BREAKER_NO_ACTION: 25
  CIRCUIT_BREAKER_TRIP: 23
  STRATEGY_CI_FAIL: 17
  LARGE_ODDS_DRIFT: 2
  ANOMALY_BET_VOLUME_DROP: 1
  ANOMALY_SCAN_FINAL_RATIO: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 38 | 8 | 11,400 | 5,100 | -6,300 | 0.447 |
| S01_NAKAANA1 | 36 | 14 | 7,200 | 6,900 | -300 | 0.958 |
| S02_TETSUBAN | 15 | 7 | 3,000 | 2,700 | -300 | 0.9 |

## 直近アラート (24h・新しい順)
```
[15:12:06] FINAL_MISSING: {"deadline": "2026-06-01T13:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060108081342", "sid": "S00"}
[15:03:42] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:03:42] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S00"}
[14:52:21] FINAL_MISSING: {"deadline": "2026-06-01T13:21:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060105041321", "sid": "S00"}
[14:50:08] FINAL_MISSING: {"deadline": "2026-06-01T14:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060105061420", "sid": "S00"}
[14:46:05] FINAL_MISSING: {"deadline": "2026-06-01T13:15:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060108071315", "sid": "S00"}
[14:43:39] FINAL_MISSING: {"deadline": "2026-06-01T09:10:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060114020910", "sid": "S00"}
[14:33:32] CIRCUIT_BREAKER_TRIP: {"cost": 11400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 5100, "roi_7d": 0.447, "sid": "S00"}
[14:12:05] FINAL_MISSING: {"deadline": "2026-06-01T13:42:00+09:00", "kind": "FINAL_MISSING", "nid": "2026060108081342", "sid": "S00"}
[14:05:06] ANOMALY_SCRAPER_FAILURE_BURST: {"failures_1h": 3, "kind": "ANOMALY_SCRAPER_FAILURE_BURST", "log_lines_1h": 912}
```

## 本日残レース: 72件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 144件 登録 / 72件 締切済
- 通知発射: scan=12 nid / final=9 nid / result=5 nid
- predictions: 6 / うち結果DB記録済: 5
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 5件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S02_TETSUBAN | 057R | win | 1 | 0.5891 | 2.6 | 1.53 | 200 | scan=2.5 drift=+4.0% | 14:53:22 |
| S02_TETSUBAN | 136R | win | 1 | 0.5735 | 2.9 | 1.66 | 200 | scan=- drift=- | 12:57:21 |
| S01_NAKAANA1 | 052R | win | 1 | 0.5735 | 3.4 | 1.95 | 200 | scan=3.4 drift=+0.0% | 12:20:25 |
| S00 | 051R | win | 1 | 0.5735 | 6.6 | 3.78 | 300 | scan=4.0 drift=+65.0% | 11:52:33 |
| S00 | 112R | win | 1 | 0.0923 | 27.7 | 2.56 | 300 | scan=5.2 drift=+432.7% | 11:05:22 |
| S01_NAKAANA1 | 142R | win | 1 | 0.5174 | 3.9 | 2.02 | 200 | scan=4.1 drift=-4.9% | 09:07:45 |
| S00 | 1510R | win | 1 | 0.4111 | 4.5 | 1.85 | 300 | scan=4.3 drift=+4.7% | 19:30:23 |
| S02_TETSUBAN | 079R | win | 1 | 0.4989 | 2.8 | 1.40 | 200 | scan=- drift=- | 19:24:22 |
| S00 | 076R | win | 1 | 0.5334 | 4.8 | 2.56 | 300 | scan=- drift=- | 18:07:31 |
| S01_NAKAANA1 | 074R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=3.9 drift=-23.1% | 17:17:22 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 45 | +17.9% | -81.4% | +432.7% | 13 | 7 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 482.1s |
| **Latency** (scan→final max) | 620.5s |
| **Traffic** (notifications 24h) | 71 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 600円 used |
| **Saturation** (S01_NAKAANA1) | 400円 used |
| **Saturation** (S02_TETSUBAN) | 400円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 349 | 0.4590 | 0.3238 | +0.1352 | 🟡+30% | 0.2339 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 174 | 0.4227 | 0.2816 | 0.2182 | 🔴-0.08 | 0.861 |
| S01_NAKAANA1 | win | 116 | 0.4845 | 0.3103 | 0.2455 | 🔴-0.15 | 0.793 |
| S02_TETSUBAN | win | 59 | 0.5155 | 0.4746 | 0.2571 | 🔴-0.03 | 0.883 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.10-0.15 | 6 | 0.1265 | 0.1667 | ✅-0.0402 |
| 0.20-0.30 | 8 | 0.2235 | 0.3750 | 🔴-0.1515 |
| 0.30-0.50 | 147 | 0.4148 | 0.2721 | 🔴+0.1426 |
| 0.50+ | 177 | 0.5396 | 0.3898 | 🔴+0.1497 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 28 | 0.77 |
| win | <5.0 | ✅learned | 55 | 0.757 |
| win | <10.0 | ✅learned | 39 | 0.52 |
| win | <20.0 | ✅learned | 11 | 0.193 |
| win | <50.0 | ⚠️fallback | 1 | 0.1 |
| win | ∞ | ⚠️fallback | 0 | 0.1 |
| 2t | <10.0 | ⚠️fallback | 0 | 0.5 |
| 2t | <30.0 | ⚠️fallback | 0 | 0.35 |
| 2t | ∞ | ⚠️fallback | 0 | 0.25 |
| 3t | <10.0 | ⚠️fallback | 1 | 0.4 |
| 3t | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3t | <200.0 | ⚠️fallback | 0 | 0.3 |
| 3t | ∞ | ⚠️fallback | 0 | 0.2 |
| 2f | <10.0 | ⚠️fallback | 0 | 0.45 |
| 2f | ∞ | ⚠️fallback | 0 | 0.3 |
| 3f | <50.0 | ⚠️fallback | 0 | 0.4 |
| 3f | ∞ | ⚠️fallback | 0 | 0.25 |

---
_auto-generated by claude_snapshot.py at 2026-06-01T15:20:01.408918+09:00_