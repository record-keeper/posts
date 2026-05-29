# ClaudeDebug スナップショット

## 🔴 現状: RED

**生成**: 2026-05-29T15:20:02.346644+09:00

### 次に取るべきアクション
> RED最優先: PSI_DRIFT_DETECTED×42 (24h) → ログ/DB確認

### 検出された問題
- 🟡 FINAL_MISSING×50 (24h)
- 🔴 PSI_DRIFT_DETECTED×42 (24h)
- 🔴 CIRCUIT_BREAKER_TRIP×32 (24h)
- 🔴 STRATEGY_CI_FAIL×17 (24h)
- 🟡 LARGE_ODDS_DRIFT×1 (24h)
- 🔴 SEND_WITHOUT_DBREC×1 (24h)
- 🔴 alert_manager dispatch 失敗確定 1件（手動確認必要）

---

## 🔧 AI デバッグキュー（このClaudeが対処）

### 🔴 CIRCUIT_BREAKER_TRIP  ×32  [2026-05-29T15:04:22]
- key: `CIRCUIT_BREAKER_TRIP|`
- **FIX**: 7日ROI<0.7→戦略を enabled:false にして原因調査。校正ドリフトか市場変化を確認

### 🔴 CIRCUIT_BREAKER_NO_ACTION  ×32  [2026-05-29T15:04:22]
- key: `CIRCUIT_BREAKER_NO_ACTION|`
- **FIX**: CIRCUIT_BREAKER_TRIP 発動済なのに strategies.json で enabled のまま。enabled:false に切替 or 復旧条件満たしたか確認

### 🔴 PSI_DRIFT_DETECTED  ×16  [2026-05-29T15:04:22]
- key: `PSI_DRIFT_DETECTED|`
- **FIX**: ml_prob 分布の PSI>0.25→モデル入力の分布シフト。校正テーブル再生成 or モデル再学習を検討

### 🔴 STRATEGY_CI_FAIL  ×16  [2026-05-29T15:04:22]
- key: `STRATEGY_CI_FAIL|`
- **FIX**: grid戦略のOOS CI下限<1.0→論文基準で赤字リスク。strategies.json確認

### 🟡 KS_ODDS_DRIFT  ×16  [2026-05-29T15:04:22]
- key: `KS_ODDS_DRIFT|`
- **FIX**: オッズ分布の KS 検定 p<0.01→市場構造変化の可能性。settlement_ratio の fallback 値を再検証

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-29T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S00 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🔴 CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION  ×1  [2026-05-29T15:00:03]
- key: `CODE_AUDIT_CIRCUIT_BREAKER_NO_ACTION|戦略 S01_NAKAANA1 が TRIP してるが enabled のまま`
- **FIX**: CIRCUIT_BREAKER_TRIP 戦略が enabled のまま。enabled:false に

### 🟡 ANOMALY_BET_VOLUME_SPIKE  ×15  [2026-05-29T14:45:37]
- key: `ANOMALY_BET_VOLUME_SPIKE|`
- **FIX**: 本日のbet数が2σ急増。filter logic緩み・戦略追加・race_schedule異常

### 🟡 ANOMALY_SCAN_FINAL_RATIO  ×11  [2026-05-29T12:18:41]
- key: `ANOMALY_SCAN_FINAL_RATIO|`
- **FIX**: scan→final成立率が7日baselineから2σ逸脱。scan/final window設定・odds取得タイミング

### 🟡 ANOMALY_SCRAPER_FAILURE_BURST  ×60  [2026-05-29T12:12:43]
- key: `ANOMALY_SCRAPER_FAILURE_BURST|`
- **FIX**: 直近1h でscraper 3-retry 全敗多発。boatrace.jp 側timeout / IP ban / DDoS

### 🔴 SEND_WITHOUT_DBREC  ×1  [2026-05-29T12:00:44]
- key: `SEND_WITHOUT_DBREC|`
- **FIX**: record_notification の例外→DB書込エラー原因特定（WAL、ロック）

### ℹ️ INSUFFICIENT_SAMPLE  ×1  [2026-05-29T06:00:11]
- key: `INSUFFICIENT_SAMPLE|S00: n=176<300 — v17 要件未達、ROI判定保留`
- **FIX**: N<300→運用継続でサンプル蓄積、数週間は判定保留

### 🟡 ORPHAN_SCAN  ×1  [2026-05-29T06:00:11]
- key: `ORPHAN_SCAN|234 件の scan に final/retreat 追従無し`
- **FIX**: scan 後 final も retreat も無い→当該レースの final 窓が短すぎ/fetch 失敗

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.30-0.40: n=26 pred=0.3234 actual=0.2308 gap=+0.0926`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-29T06:00:11]
- key: `DRIFT_BUCKET|drift ≥+30%: n=35 hit%=20.0% ROI=0.57 (コスト 9,000/回収 5,090)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.00-0.05: n=16 pred=0.0095 actual=0.0625 gap=-0.0530`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.15-0.20: n=5 pred=0.1957 actual=0.2000 gap=-0.0043`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ CALIBRATION_LIVE  ×1  [2026-05-29T06:00:11]
- key: `CALIBRATION_LIVE|decile 0.20-0.30: n=12 pred=0.2234 actual=0.4167 gap=-0.1933`
- **FIX**: bt別の予測確率vs実的中率の定期報告。判定ではなく参照用

### ℹ️ DRIFT_BUCKET  ×1  [2026-05-29T06:00:11]
- key: `DRIFT_BUCKET|drift -30%〜-10%: n=38 hit%=28.9% ROI=1.03 (コスト 8,600/回収 8,840)`
- **FIX**: ドリフト帯別 ROI 分析の情報。対策検討の材料

### ℹ️ ROI_STAT  ×1  [2026-05-29T06:00:11]
- key: `ROI_STAT|S00: n=176 hit%=28.4% hit_CI[Bonf]=[19.7,39.0]% ROI=0.96 ROI_boot95=[0.68,1.28]`
- **FIX**: 統計サマリ情報。判定ではなく参照用


以下、詳細セクション（通常読み飛ばし可）

## 環境・コード状態
- git_sha: `<error: Command '['git', '-C', '/opt/boa` dirty=True
- config.json md5: `eb532e851a30cd2f7e69bdf0dfca3f2b`
- strategies.json md5: `06b22dd935785e7947bf9c0f170b69a3`
- numpy=2.4.4 lightgbm=4.6.0 scipy=1.17.1
- **calibration_applied**: True ← predictor.py が校正を呼んでるか
- DB: 3.74MB / last modified 2026-05-29T15:19:43.435510+09:00

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
'B': 100} default=100
2026-05-29 15:19:05,905 [INFO] run_cycle: daily_limit_by_trust={'S': 15000, 'A': 6000, 'B': 1500} default=5000
2026-05-29 15:19:05,972 [INFO] predictor: Models loaded OK
2026-05-29 15:19:17,116 [WARNING] scraper: fetch error (1/3): https://www.boatrace.jp/owpc/pc/race/racelist?rno=10&jcd=02&hd=20260529: HTTPSConnectionPool(host='www.boatrace.jp', port=443): Read timed out. (read timeout=10), retry in 1s
2026-05-29 15:19:28,512 [INFO] scraper: odds3t: 120/120 parsed
2026-05-29 15:19:29,619 [INFO] scraper: odds3f: 20/20 parsed
2026-05-29 15:19:30,726 [INFO] scraper: odds2t: 30/30 parsed
2026-05-29 15:19:30,728 [INFO] scraper: odds2f: 15/15 parsed
2026-05-29 15:19:31,836 [INFO] scraper: odds_win: 6/6 parsed
2026-05-29 15:19:31,836 [INFO] scraper: fetch_race 02/10: boats=6 odds=191/191
2026-05-29 15:19:31,841 [INFO] predictor: CALIBRATION_MODE=on
2026-05-29 15:19:31,841 [INFO] predictor: combos: {'win': 6, '2t': 30, '3t': 120}
2026-05-29 15:19:31,847 [INFO] run_cycle: fetched 02/10 [final]: 156 combos
2026-05-29 15:19:34,200 [WARNING] scraper: beforeinfo parse failed: jcd=03 rno=10
2026-05-29 15:19:34,200 [WARNING] run_cycle: fetch None: 03/10
2026-05-29 15:19:36,435 [WARNING] scraper: beforeinfo parse failed: jcd=01 rno=1
2026-05-29 15:19:36,435 [WARNING] run_cycle: fetch None: 01/1
2026-05-29 15:19:39,744 [INFO] scraper: odds3t: 120/120 parsed
2026-05-29 15:19:40,884 [INFO] scraper: odds3f: 20/20 parsed
2026-05-29 15:19:41,965 [INFO] scraper: odds2t: 30/30 parsed
2026-05-29 15:19:41,966 [INFO] scraper: odds2f: 15/15 parsed
2026-05-29 15:19:43,064 [INFO] scraper: odds_win: 3/6 parsed
2026-05-29 15:19:43,064 [INFO] scraper: fetch_race 15/1: boats=6 odds=188/191
2026-05-29 15:19:43,076 [INFO] predictor: CALIBRATION_MODE=on
2026-05-29 15:19:43,077 [INFO] predictor: combos: {'win': 3, '2t': 30, '3t': 120}
2026-05-29 15:19:43,086 [INFO] run_cycle: fetched 15/1 [scan]: 153 combos
2026-05-29 15:19:43,403 [INFO] run_cycle: run_cycle done: 0 notifications

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
    "c": 86
  },
  {
    "target": "primary",
    "ok": 1,
    "c": 86
  }
]
```

## Phase別通知記録 (24h)
{'final': 35, 'result': 21, 'scan': 30}

## アラート件数 (24h・種類別)
```
  ANOMALY_SCRAPER_FAILURE_BURST: 140
  FINAL_MISSING: 50
  KS_ODDS_DRIFT: 42
  PSI_DRIFT_DETECTED: 42
  CIRCUIT_BREAKER_TRIP: 32
  CIRCUIT_BREAKER_NO_ACTION: 19
  STRATEGY_CI_FAIL: 17
  ANOMALY_BET_VOLUME_SPIKE: 8
  ANOMALY_SCAN_FINAL_RATIO: 7
  LARGE_ODDS_DRIFT: 1
  SEND_WITHOUT_DBREC: 1
```

## 戦略別 ROI (7日)
| sid | n | hits | cost | payout | PL | ROI |
|---|---|---|---|---|---|---|
| S00 | 31 | 5 | 9,300 | 4,680 | -4,620 | 0.503 |
| S01_NAKAANA1 | 38 | 9 | 7,600 | 4,460 | -3,140 | 0.587 |
| S02_TETSUBAN | 11 | 7 | 2,200 | 2,880 | +680 | 1.309 |

## 直近アラート (24h・新しい順)
```
[15:04:22] STRATEGY_CI_FAIL: {"ci_lo": null, "kind": "STRATEGY_CI_FAIL", "sid": "S02_TETSUBAN"}
[15:04:22] CIRCUIT_BREAKER_NO_ACTION: {"kind": "CIRCUIT_BREAKER_NO_ACTION", "sid": "S01_NAKAANA1"}
[14:51:39] FINAL_MISSING: {"deadline": "2026-05-29T12:20:00+09:00", "kind": "FINAL_MISSING", "nid": "2026052923091220", "sid": "S00"}
[14:45:37] CIRCUIT_BREAKER_TRIP: {"cost": 7600, "kind": "CIRCUIT_BREAKER_TRIP", "n": 38, "payout": 4460, "roi_7d": 0.587, "sid": "S01_NAKAANA1"}
[14:45:37] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.002665, "ks_stat": 0.23}
[14:45:37] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 245, "n_recent": 80, "psi": 0.58}
[14:45:37] ANOMALY_BET_VOLUME_SPIKE: {"baseline_mean": 6.7, "baseline_n_days": 7, "baseline_stdev": 2.6, "hour": 14, "kind": "ANOMALY_BET_VOLUME_SPIKE", "today_so_far": 12, "z_score": 2.01}
[14:42:30] CIRCUIT_BREAKER_TRIP: {"cost": 7400, "kind": "CIRCUIT_BREAKER_TRIP", "n": 37, "payout": 4460, "roi_7d": 0.603, "sid": "S01_NAKAANA1"}
[14:42:30] KS_ODDS_DRIFT: {"kind": "KS_ODDS_DRIFT", "ks_p": 0.003038, "ks_stat": 0.229}
[14:42:30] PSI_DRIFT_DETECTED: {"bt": "win", "kind": "PSI_DRIFT_DETECTED", "n_baseline": 245, "n_recent": 79, "psi": 0.583}
```

## 本日残レース: 65件

## 本日nidレジャー（ID単位完遂突合せ）
- race_schedule: 168件 登録 / 103件 締切済
- 通知発射: scan=19 nid / final=20 nid / result=11 nid
- predictions: 12 / うち結果DB記録済: 12
- ✅ 結果DBあるが通知未発射: 0件 `tools/backfill_result_notifications.py` で救済可
- 🔴 scan後final無しのまま締切: 4件（FINAL_MISSING の温床）

## 直近送信失敗 (24h)
```
```

## 最新 predictions サンプル (計算spot-check用)
| sid | race | bt | combo | p | odds | ev | bet | at |
|---|---|---|---|---|---|---|---|---|
| S01_NAKAANA1 | 029R | win | 1 | 0.5123 | 3.0 | 1.54 | 200 | scan=- drift=- | 14:45:32 |
| S01_NAKAANA1 | 096R | win | 1 | 0.4111 | 3.1 | 1.27 | 200 | scan=4.0 drift=-22.5% | 12:55:21 |
| S00 | 238R | win | 1 | 0.3177 | 27.7 | 8.80 | 300 | scan=- drift=- | 11:45:32 |
| S00 | 147R | win | 1 | 0.5735 | 6.3 | 3.61 | 300 | scan=13.0 drift=-51.5% | 11:29:21 |
| S00 | 093R | win | 1 | 0.5109 | 10.1 | 5.16 | 300 | scan=4.1 drift=+146.3% | 11:26:19 |
| S01_NAKAANA1 | 237R | win | 1 | 0.5123 | 3.3 | 1.69 | 200 | scan=4.5 drift=-26.7% | 11:18:34 |
| S00 | 146R | win | 1 | 0.5174 | 6.7 | 3.47 | 300 | scan=5.2 drift=+28.8% | 11:00:25 |
| S01_NAKAANA1 | 112R | win | 1 | 0.5735 | 3.0 | 1.72 | 200 | scan=- drift=- | 10:57:44 |
| S00 | 112R | win | 1 | 0.5735 | 5.2 | 2.98 | 300 | scan=- drift=- | 10:56:33 |
| S01_NAKAANA1 | 236R | win | 1 | 0.5123 | 3.2 | 1.64 | 200 | scan=- drift=- | 10:47:33 |

## オッズドリフト統計 (7日)

| bt | n | avg | min | max | down10 | collapse(≤-30%) | any_large(≥10%) |
|---|---|---|---|---|---|---|---|
| win | 45 | -1.9% | -81.4% | +157.5% | 17 | 10 | 32 |

## 校正テーブル合格状況

- total: 27 グループ
- passed: 19
- failed: 8 — `2f|4, 2f|5, 3f|2, 3f|3, 3f|4, 3t|1, 3t|4, 3t|5`
- 主力グループ状態: ✅ (全12グループ合格)

## SRE Golden Signals (24h)

| Signal | Value |
|---|---|
| **Latency** (scan→final avg) | 448.6s |
| **Latency** (scan→final max) | 622.7s |
| **Traffic** (notifications 24h) | 86 |
| **Errors** (send fail rate) | ✅ 0.0% |
| **Saturation** (S00) | 1,800円 used |
| **Saturation** (S01_NAKAANA1) | 1,200円 used |

## 信ぴょう性メトリクス（予測精度の証拠）

### bt別: 予測確率 vs 実的中率
| bt | n | 予測avg | 実的中率 | 校正誤差 | 過信度 | Brier |
|---|---|---|---|---|---|---|
| 3t | 12 | 0.0019 | 0.0833 | -0.0814 | ✅-4200% | 0.0819 |
| win | 325 | 0.4563 | 0.3169 | +0.1393 | 🟡+30% | 0.2354 |

### 戦略別: 校正精度 + Brier Skill Score
| sid | bt | n | pred | actual | Brier | BSS | ROI |
|---|---|---|---|---|---|---|---|
| S00 | win | 176 | 0.4243 | 0.2784 | 0.2242 | 🔴-0.12 | 0.946 |
| S01_NAKAANA1 | win | 98 | 0.4852 | 0.2959 | 0.2451 | 🔴-0.18 | 0.776 |
| S02_TETSUBAN | win | 51 | 0.5110 | 0.4902 | 0.2555 | 🔴-0.02 | 0.933 |
| S04_SELL_3T | 3t | 12 | 0.0019 | 0.0833 | 0.0819 | 🔴-0.07 | 0.617 |

### 確率デシル別: 校正カーブ
| 確率帯 | n | 予測avg | 実的中率 | gap |
|---|---|---|---|---|
| 0.00-0.05 | 16 | 0.0095 | 0.0625 | 🔴-0.0530 |
| 0.15-0.20 | 5 | 0.1957 | 0.2000 | ✅-0.0043 |
| 0.20-0.30 | 11 | 0.2239 | 0.4545 | 🔴-0.2306 |
| 0.30-0.50 | 140 | 0.4158 | 0.2786 | 🔴+0.1372 |
| 0.50+ | 159 | 0.5400 | 0.3648 | 🔴+0.1752 |

## Settlement Ratio データ品質

- 学習済み: 4バンド / fallback: 13バンド
| bt | odds帯 | source | n | ratio |
|---|---|---|---|---|
| win | <3.0 | ✅learned | 25 | 0.783 |
| win | <5.0 | ✅learned | 45 | 0.8 |
| win | <10.0 | ✅learned | 37 | 0.538 |
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
_auto-generated by claude_snapshot.py at 2026-05-29T15:20:02.346644+09:00_